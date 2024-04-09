# rete js

<aside>
💡 **rete.js**

1. Plugin System - Scope & Pipe
    1. scope = node
    2. pipe = connection / socket?
    3. 전달되는 값 = signal (context)
    4. parent에 파이프가 있고 여기 1을 내보낸다면
        1. 이때 parent.use(Child)했다면
        2. parent도 emit 1, child도 emit 1
2. ClassicPreset
    1. 
3. Node
    1. Control
        1. component
            1. 
        2. constructor
            1. parameter 
                1. emitter
                2. key
                3. node = component
                4. readonly
            2. attribute
                1. emitter
                2. key
                3. component
                4. props
        3. setValue
    2. Component
        1. constructor
            1. parameter = type
            2. attribute
                1. node_id
                2. filter_type
                3. state
        2. builder(node)
            1. input (인풋소켓 만들어주기 = `new Rete.Input(어쩌구, 저쩌구, socket);`
            2. output (아웃풋소켓 만들어주기 = `new Rete.Output(어쩌구, 저쩌구, socket);`
            3. ctrl (컨트롤 만들어주기 아까 만든 클래스 사용 = `new LiverControl(this.editor, 어쩌구, node;`
            4. node id 만들어주고
            5. 만든거 다 붙여서 리턴 `node.addControl(ctrl).addInput(in1).addOutput(out1)`
        3. Worker
            1. parameter 
                1. node
                2. inputs
                3. outputs
            2. attribute

```tsx
//개념
// 플러그인 시스템 -> editor(노드, 커넥션) -> area(시각화) -> connection(인터랙션)/render(리액트렌더)/contextMenu(우클릭메뉴)

// 데이터 구조
import { ClassicPreset, NodeEditor, BaseSchemes, GetSchemes } from 'rete';
// const { Node, Connection, Socket, Input, InputControl, Output, Control, Port } = ClassicPreset

/**
 * Node(label)
 * Connection(source, sourceOutput-포트키, target, targetInput-포트키)
 * 
 * Socket(name)
 * Input(socket, label, multipleConnections)
 * Output(socket, label, multipleConnections)
 * 
 * Control()
 * InputControl(type, options)
 * 
 * Port(socket, label, multipleConnections)
 */

// 인터랙션 (줌, 드래그 등, + 다른 플러그인을 연결해주는 플러그인)
import { BidirectFlow, ConnectionPlugin, Presets as ConnectionPresets } from 'rete-connection-plugin'
import { AreaPlugin, AreaExtensions  } from 'rete-area-plugin';
// const connection = new ConnectionPlugin<Schemes, AreaExtra>()
// connection.addPreset(ConnectionPresets.classic.setup())

// 렌더링
import { ClassicScheme, ReactArea2D, ReactPlugin, Presets as ReactPresets } from 'rete-react-plugin'
import { MinimapExtra } from 'rete-minimap-plugin';
import { ContextMenuExtra } from 'rete-context-menu-plugin';
import { useEffect } from 'react';

// 데이터플로우 엔진
import { DataflowEngine, ControlFlowEngine } from 'rete-engine'
import * as RE from"rete-engine";

function App() {
  const start = async () => {

    // ---- 에디터 ---- 'rete'
    type Schemes = ClassicScheme;
    // type Schemes = BaseSchemes;
    const editor = new NodeEditor<Schemes>();

    const socket = new ClassicPreset.Socket('socketName');

    const node1 = new ClassicPreset.Node('Label');
    node1.addOutput('output', new ClassicPreset.Output(socket, 'Title1'));
    // > node.addOutput("portKey", Output객체);
    console.log(node1);
    await editor.addNode(node1);

    const node2 = new ClassicPreset.Node('Label');
    node2.addOutput('output', new ClassicPreset.Output(socket, 'Title2'));
    node2.addInput('input', new ClassicPreset.Input(socket, 'Title3'));
    // > node.addInput("portKey", Input객체);
    await editor.addNode(node2);

    const connection = new ClassicPreset.Connection(node1, 'output', node2, 'input');
    // > new ClassicPreset.Connection(sourceNode, 'portKey', targetNode, 'portKey')
    await editor.addConnection(connection);
    // > await editor.removeConnection(connection.id);

    // ---- 2D Area ---- 'rete-area-plugin'
    // 시각화 단계
    type AreaExtra =
    | ReactArea2D<Schemes>
    | ContextMenuExtra
    | MinimapExtra
    // > 이 타입은 다른 종류의 시그널 타입들을 통합하는데 필요
    const container = document.getElementById('App') as HTMLElement;
    const area = new AreaPlugin<Schemes, AreaExtra>(container);
    // > container (담을 HTMLElement 필요)
    // 플러그인 + 확장 연결 기능
    AreaExtensions.selectableNodes(area, AreaExtensions.selector(), {
    accumulating: AreaExtensions.accumulateOnCtrl()
    });

    // ---- 커넥션과 상호작용 ---- 'rete-connection-plugin'
    // 생성 삭제와 같은 사용자 상호작용 담당
    const connectionPlugin = new ConnectionPlugin<Schemes, AreaExtra>();
    connectionPlugin.addPreset(ConnectionPresets.classic.setup())

    // ---- 렌더링 ---- 'rete-react-plugin'
    const reactPlugin = new ReactPlugin<Schemes, AreaExtra>()
    reactPlugin.addPreset(ReactPresets.classic.setup());
    reactPlugin.addPreset(ReactPresets.contextMenu.setup());
    reactPlugin.addPreset(ReactPresets.minimap.setup());
    area.use(reactPlugin);

    // ---- 엔진 ---- 'rete-engine'
    // data-flow & control-flow
    /** data-flow
     * 오직 데이터에 집중 
     * 
     * data()
     * > 받는 노드가 들어오는 노드로부터 데이터를 "요청"
     * > 그럼 받은 데이터를 토대로 DataflowEngine이 C라는 데이터를 만들어서 fetch() 해줌
     * 
     * 
     * */ 
    class NodeAdd extends ClassicPreset.Node<{ left: ClassicPreset.Socket, right: ClassicPreset.Socket }, { value: ClassicPreset.Socket }, { }>{
	    constructor() {
	        super("NodeAdd");
	        // init controls and ports
	    }
	    // mandatory method
	    data(inputs: { left?: number[], right?: number[] }): { value: number } {
	        const left = inputs.left[0] || 0
	        const right = inputs.right[0] || 0
	    return {
	        value: left + right
	        }
	    }
    }
    const nodeAdd = new NodeAdd();
    type Schemes2 = RE.DataflowEngineScheme;
    const engine = new DataflowEngine<Schemes2>();
    editor.use(engine);
    const nodeOutput = await engine.fetch(node2.id);

    /** control-flow
     * 제어를 넘겨줌 
     * 어떻게 넘겨줄지를 다음노드에게 전달해 
     * 
     * execute()
     * > A: 먼가를 해서 컨트롤을 B로 전달
     * > B: 컨트롤을 C 혹은 D에게 보낼수도, 둘 다 보낼수도 있음
     * > C&D: 더이상 연결된 노드 없어도 먼가 함
     * */ 
    class Log extends ClassicPreset.Node<{ enter: ClassicPreset.Socket }, { out: ClassicPreset.Socket }, {}> {
    constructor() {
        super("NodeLog");
        // init ports
    }
    // mandatory method
    execute(input: 'enter', forward: (output: 'out') => void) {
        console.log('log something')
        forward('out')
    }
    }
    const logNode = new Log();
    type Schemes3 = RE.ControlFlowEngineScheme;
    const engine2 = new ControlFlowEngine<Schemes3>()
    editor.use(engine2);
    engine.execute(logNode.id)
}

useEffect(()=>{
    start();
}, [])
return (
    <div className="App" id="App"></div>
);
}

export default App;
```

예시 코드 Basic

```tsx
import { createRoot } from "react-dom/client";

// 데이터 구조
import { ClassicPreset, NodeEditor, GetSchemes } from 'rete';
// const { Node, Connection, Socket, Input, InputControl, Output, Control, Port } = ClassicPreset

/**
 * Node(label)
 * Connection(source, sourceOutput-포트키, target, targetInput-포트키)
 * 
 * Socket(name)
 * Input(socket, label, multipleConnections)
 * Output(socket, label, multipleConnections)
 * 
 * Control()
 * InputControl(type, options)
 * 
 * Port(socket, label, multipleConnections)
 */

// 인터랙션 (줌, 드래그 등, + 다른 플러그인을 연결해주는 플러그인)
import { ConnectionPlugin, Presets as ConnectionPresets } from 'rete-connection-plugin'
import { AreaPlugin, AreaExtensions  } from 'rete-area-plugin';
// const connection = new ConnectionPlugin<Schemes, AreaExtra>()
// connection.addPreset(ConnectionPresets.classic.setup())

// 렌더링
import { ClassicScheme, ReactArea2D, ReactPlugin, Presets as ReactPresets } from 'rete-react-plugin'
import { MinimapExtra } from 'rete-minimap-plugin';
import { ContextMenuExtra } from 'rete-context-menu-plugin';
import { useEffect } from 'react';

// 데이터플로우 엔진
import { DataflowEngine, ControlFlowEngine } from 'rete-engine'
import * as RE from"rete-engine";

// 1. 타입을 정의
type Schemes = GetSchemes<
ClassicPreset.Node,
ClassicPreset.Connection<ClassicPreset.Node, ClassicPreset.Node>
>;

// 2. 리액트로 렌더링 하기 위한 area 만들기
type AreaExtra =
ReactArea2D<Schemes>
| ContextMenuExtra
| MinimapExtra;

export async function createEditor(container: HTMLElement) { // useRete 할때 ref로 받는건가봐~!~
    // 1-2. 하고 에디터를 초기화하기
    const editor = new NodeEditor<Schemes>();

    // 3-2. area 설정
    const area = new AreaPlugin<Schemes, AreaExtra>(container);
    const render = new ReactPlugin<Schemes, AreaExtra>({ createRoot });

    render.addPreset(ReactPresets.classic.setup());
    editor.use(area);
    area.use(render);

    // 6. 인터랙티브 커넥션
    const connection = new ConnectionPlugin<Schemes, AreaExtra>();
    // > 보통 맨 위에 ㅇㅇ

    connection.addPreset(ConnectionPresets.classic.setup())
    area.use(connection);

    // 8. 셀렉터블 노드
    AreaExtensions.selectableNodes(area, AreaExtensions.selector(), {
        accumulating: AreaExtensions.accumulateOnCtrl()
    });

    // 9. 노드 순서 
    AreaExtensions.simpleNodesOrder(area);

    // 4. 자의적인(?) 노드 만들기
    const socket = new ClassicPreset.Socket("socket");
    const nodeA = new ClassicPreset.Node("A");
    nodeA.addControl("a", new ClassicPreset.InputControl("text", {}));
    nodeA.addOutput("a", new ClassicPreset.Output(socket));
    await editor.addNode(nodeA);

    const nodeB = new ClassicPreset.Node("B");
    nodeB.addControl("b", new ClassicPreset.InputControl("text", {}));
    nodeB.addInput("b", new ClassicPreset.Input(socket));
    await editor.addNode(nodeB);
    // 4. 커넥션 추가하기
    await editor.addConnection(new ClassicPreset.Connection(nodeA, "a", nodeB, "b"));
    // 5. 노드 포지셔닝
    await area.translate(nodeA.id, { x: 0, y: 0 });
    await area.translate(nodeB.id, { x: 270, y: 0 });

    // 7. 핏 뷰포트
    setTimeout(() => {
        // wait until nodes rendered because they dont have predefined width and height
        AreaExtensions.zoomAt(area, editor.getNodes());
    }, 10);

    return {
        destroy: () => area.destroy()
    };
}
```

예시코드 정리본

```tsx
import { createRoot } from "react-dom/client";

import { NodeEditor } from 'rete';
// Schemes라는 type을 getSchemes를 통해서 정의,
// 에디터 초기화
// 렌더링 될 area를 설정하고
// 이 때 어떤 Shemes인지, extra로 2D인지 머시긴지 type으로 넣어주기
// 렌더
// 인터랙션을 위한 플러그인을 생성하고
// 정렬 등을 해놓기
// 노드를 생성하고
// 에디터에 노드를 추가하기
// 추가된 노드들을 연결하고
// 에디터에 연결을 추가하기
// 노드의 위치를 조정하고
// 인터랙션 플러그인을 사용해서 줌엣 (카메라 초점 맞추기)

import { ClassicPreset, GetSchemes } from "rete";
import { AreaExtensions, AreaPlugin } from 'rete-area-plugin';
import { ReactArea2D, ReactPlugin, Presets } from 'rete-react-plugin';
import { ConnectionPlugin, Presets as ConnectionPresets } from 'rete-connection-plugin';

type Schemes = GetSchemes<
    ClassicPreset.Node, // 이 스킴에는 노드와
    ClassicPreset.Connection<ClassicPreset.Node, ClassicPreset.Node> // 노드들이 연결된 커넥션이 존재합니다~
>
type AreaExtra = ReactArea2D<Schemes>;

export async function createEditor2(container: HTMLElement) {
    // 각 객체 생성
    const editor = new NodeEditor<Schemes>();
    const area = new AreaPlugin<Schemes, AreaExtra>(container);
    const render = new ReactPlugin<Schemes, AreaExtra>({ createRoot });
    const connection = new ConnectionPlugin<Schemes, AreaExtra>();

    // 초기 설정
    editor.use(area);
    area.use(connection);
    area.use(render);
    render.addPreset(Presets.classic.setup());
    connection.addPreset(ConnectionPresets.classic.setup());

    AreaExtensions.simpleNodesOrder(area);
    AreaExtensions.selectableNodes(area, AreaExtensions.selector(), {
        accumulating: AreaExtensions.accumulateOnCtrl()
    });

    // 노드 생성
    const nodeA = new ClassicPreset.Node("nodeA");
    const nodeB = new ClassicPreset.Node("nodeB");
    const nodeC = new ClassicPreset.Node("nodeC");
    const socket = new ClassicPreset.Socket("socket");

    nodeA.addOutput("output", new ClassicPreset.Output(socket));
    nodeA.addControl("number", new ClassicPreset.InputControl("number", { initial: "2"}));

    nodeB.addOutput("output", new ClassicPreset.Output(socket));
    nodeB.addControl("number", new ClassicPreset.InputControl("number", { initial: "3"}));

    nodeC.addInput("input", new ClassicPreset.Input(socket));
    nodeC.addControl("number", new ClassicPreset.InputControl("number", { initial: "3"}));

    await editor.addNode(nodeA);
    await editor.addNode(nodeB);
    await editor.addNode(nodeC);
    await editor.addConnection(new ClassicPreset.Connection(nodeA, "output", nodeC, "input"));
    await editor.addConnection(new ClassicPreset.Connection(nodeB, "output", nodeC, "input"));

    // 노드 및 카메라 위치조정
    await area.translate(nodeA.id, {x:0, y:0});
    await area.translate(nodeB.id, {x:0, y:270});
    await area.translate(nodeC.id, {x:270, y:100});
    setTimeout(()=>{
        AreaExtensions.zoomAt(area, editor.getNodes());
    })

    return {
        destroy: () => area.destroy()
    };
}
```

App.tsx에서 editor 쓰는 법

```
import { createEditor2 } from "./editor2";
import { useRete } from "rete-react-plugin";

export default function App() {
  const [ref, editor] = useRete(createEditor2);

  return (
    <div className="App">
      <div ref={ref} style={{ height: "100vh", width: "100vw" }}></div>
    </div>
  );
}
/**
 * 렌더링을 위해서는 useRete 훅을 사용해야합니다.
 * 이 훅은 에디터를 HTML에 묶는 boilerplate code에 대한 필요를 제거합니다.
 * 이것은 특히 에디터의 오래된 인스턴스가 제거되고 새로운 것으로 교체되는 등의 
 * 동적으로 앱을 업데이트 하는데에 중요해졌습니다. 
 * 
 * createEditor함수는 destroy 메서드를 가진 객체를 반환해야합니다. 
 * 대개 area.destory()가 호출됩니다.
 */
```

</aside>

<aside>
💡 rete

1. 렌더링
    
    ```jsx
    const render = new ReactPlugin<Schemes, AreaExtra>({ createRoot })
    ```
    
2. 컨트롤 커스텀 렌더링
    1. 
    
    ```jsx
    render.addPreset(Presets.Classic.setup({
    	customize: {
    		node(context) {}, // 얘는 노드 렌더링 할때
    		control(context) {// 얘는 컨트롤 렌더링할때
    			// 이 안에서 payload에 따라서 반환하는 걸 다르게 하면 됨
    			// 분기 없이 바로 선언해놓은 커스텀 노드를 반환해버리면 커스텀 노드들로 다 바뀜 
    			if (context.payload.label === "white") {
    				// 그럼 선언할 때 Node("white") 했던 애들로 필터되겟지
    				// 걔네에 대해서는 다른 노드를 반환하겠다.
    				return StyledNode; // 정의해놨다면 쓰는거지.
    			}
    		}, 
    	}
    });
    ```
    
3. LiverNode = input, output, control로 구성됨.
    1. 노드 안에 data라는 함수는 input을 받아서 output을 리턴함 
    2. 그 중 control은 ui 즉 liverComponent에서 변화가 생기면 onChange ⇒  process ⇒ engine.fetch
</aside>

<aside>
💡 **boilerplate code**, = 아주 조금 혹은 아예 없는 정도의 차이를 가진 반복되는 코

</aside>

<aside>
💡 **d3+rete연결하기**

1. 두 프로젝트에서 구현한 컴포넌트를 연결 하던 중
2. 두 프로젝트에 설치된 패키지의 버전이나 종류가 달라서 똑같은 코드인데 d3에서는 되고, rete에서는 에러가 터지거나 반대의 상황 발생
3. 오류 1:
    1. 가장 명시적인 오류
    2. 임포트 해올때 파일 확장자를 쓰는지 여부
    3. 원인: tsconfig파일 내용
        1. ts파일을 compile할 때 사용하는 tsconfig 파일에서
        2. react-jsx를 사용할거라고 수정하기
        3. jsx: react-jsx
4. 오류2 :
    1. 타입 명시
    2. 창우님 폴더를 다운로드해온 rete-practice에서는 type을 명시해주지 않으니까 오류가 뫄뫄뫅 발생했다.
    3. 내가 만든 프로젝트는
    4. npm i typescript, npm i d3만 했었지만, rete-practice의 package.json을 보면
        1. 다음과 같았음 (주석처리는 같았던 부분)
            
            ```
            //"@testing-library/jest-dom": "^5.17.0",
            //"@testing-library/react": "^13.4.0",
            //"@testing-library/user-event": "^13.5.0",
            "@types/jest": "^27.5.2",
            "@types/node": "^16.18.68",
            "@types/openseadragon": "^3.0.10",
            "@types/react": "^18.2.45",
            "@types/react-dom": "^18.2.17",
            "axios": "^1.6.2",
            //"d3": "^7.8.5",
            "openseadragon": "^4.1.0",
            //"react": "^18.2.0",
            //"react-dom": "^18.2.0",
            //"react-scripts": "5.0.1",
            "rete": "^2.0.2",
            "rete-area-plugin": "^2.0.1",
            "rete-auto-arrange-plugin": "^2.0.0",
            "rete-connection-plugin": "^2.0.0",
            "rete-context-menu-plugin": "^2.0.0",
            "rete-engine": "^2.0.0",
            "rete-react-plugin": "^2.0.4",
            "rsuite": "^5.47.0",
            "sass": "^1.69.5",
            "styled-components": "^6.1.1",
            "typescript": "^4.9.5", // 버전이 d3는 5.0.1
            //"web-vitals": "^2.1.4"
            ```
            
        2. (아니 d3 예제그대로 복붙해온거였는데)
        3. 아마 `@types/react`나 typescript 버전 차이 때문으로 추정 중
    5. 예시 코드
        1. 32개의 키를 가진 객체를 만들어야 했었는데
        2. 이렇게 만들엇었다면
            
            ```tsx
            // 테스트 데이터 만들어주기
            export const data = [{}];
            testFeature.forEach((v, i) => {
              data[0][`${i+1}`] = v;
            })
            data[0]["group"] = 4;
            ```
            
        3. 이렇게 만들어야 했따.
            
            ```tsx
            // 테스트 데이터 만들어주기
            export const data: Data = [];
            const testData: Record<string, number> = {}
            testFeature.forEach((v:number, i:number) => {
              testData[`${i}`] = v;
            })
            testData.group = testLabel;
            data.push(testData);
            ```
            
            1. data 배열안에 들어갈 객체 타입도
            2. forEach에 들어갈 v와 i도 number라고 명시를 해줬따!!
5. 오류3: 타입 명시2
    1. d3 메서드를 이용할 때도 인자로 넣어주는 값들의 타입을 맞춰줘야했다. 
    2. 안 그러면 any 타입은 string으로 들어갈 수 없다 거나 
    3. 아님 number 타입 인데 string이라 거나
    4. 타입 오류로 에러가 났다. 
    5. 예시 코드
        1. 기존
            
            ```tsx
            return <path 
            	key={i} 
            	d={d} 
            	stroke={colorScale(series.group)} 
            	fill="none" 
            />;
            ```
            
        2. 바꾼 거
            
            ```tsx
            return <path 
            	key={i} 
            	d={d} 
            	stroke={colorScale(series.group.toString())} 
            	fill="none" 
            />;
            ```
            
</aside>

<aside>
💡 module.css

1. 개념: 
2. 특징: 
    1. jsx 파일에서 css파일을 import 해올때,
    2. css 파일 내에서 선언한 css 클래스가 
    3. 모두 고유해져 파일간 선택자가 중첩되는 것을 완벽히 방지
    4. 고유 이름을 만드는 과정에서 파일 경로, 이름, 클래스 이름, 해쉬값 등이 사용될 수도 있음
    5. 아닐 수도 있음 : 
    6. 컴포넌트마다 스타일링을 하기 위해 사용함 
3. 사용법:
    1. import styles from “./dsdfsd.module.css”
    2. ~ className={styles.Box}
4. 주의사항:
    1. typescript에서 사용하려고 하면 모듈로 인식하지 못해서 오류가 발생
    2. 해결방법
        1. src 폴더 내에 global.d.ts 파일 생성
        2. 파일 내에 아래 내용 작성declare module "*.scss" 
            
            ```tsx
            {
              const content: { [className: string]: string };
              export = content;
            }
            ```
            
        
</aside>

<aside>
💡 **리팩토링**

1. 사이드 패널
    1. 기존:
        1. `area.addPipe()`: 사이드 패널 컴포넌트 안에서 노드 ID를 받아옴
        2. `editor.getNode(nodeId)`: 받아온 아이디가 바뀔때마다 editor안에서 노드를 찾음
    2. 변경사항
        1. `getPanelContent(type, ctrl)`: 선택된 노드에 따라 다른 컴포넌트를 반환하도록 함수로 분리
        2. 선택된 노드의 라벨에 따라 다른 Viewer 컴포넌트를 반환할 때, Viewer 컴포넌트에 전달되는 props의 형태를 수정
            1. As-is: { dir: 데이터가 저장된 폴더명, path: 데이터가 저장된 경로, server: 데이터가 저장된 서버명, width, height} 
                1. 선택된 노드의 node.control.ctrl.value.path를 Viewer의 props중 일부로 전달
            2. To-be: 
                1. 선택된 노드의 contol.ctrl 자체를 전달하고
                2. 이후 데이터 처리는 전달 받은 컴포넌트 안에서 수행
            3. 이유: 
                1. 상위 컴포넌트인 사이드패널은 분기처리만으로도 이미 코드가 충분히 복잡했음. 
                2. 데이터를 사용할 컴포넌트에서 직접 데이터를 처리하는게 표시해야할 데이터가 어떤 형태인지 파악하기에도 더 용이할 것이라 판단.
2. 챠트 뷰어
    1. 기존: 
        1. {x: 0, y:0} 형태의 객체로 이루어진 배열을 Props로 전달 받아서 히스토그램을 그리는 컴포넌트
        
    2. 변경사항:
        1. Control 자체를 전달받아서
        2. Control.value를 가지고
        3. useGetDataChart()를 통해 데이터를 받아오도록 함
3. useGetData4Chart, useGetData4Feature 훅
    1. 새로 생성
    2. 내용:
        1. getData4Chart 라는 기존에 api와 통신해서 여러 데이터를 받아오던 함수를 두 개의 훅으로 분리하여 동기적으로 데이터를 받아올 수 있도록 만듦
</aside>

![alt text](/99_images/retepractice.png)