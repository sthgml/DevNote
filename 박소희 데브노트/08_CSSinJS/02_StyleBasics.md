# Style Basics

## 👉 [강의 보기]

## 학습 키워드

- className
- 의미있는 마크업

<aside>
💡 의미있는 마크업을 하기 위해서는 HTML Element 들이 어떤 의미를 가지고 있는지 정확하게 알고 있어야 합니다. 레퍼런스를 참고하여 HTML 마크업에 대해 정확하게 이해한 뒤 정리하고 넘어가시면 좋습니다.
참고 레퍼런스: https://developer.mozilla.org/ko/docs/Web/HTML/Reference
</aside>

id = html 내에서 하나만 존재해야됨 (웹표준)
증거 (document.getElementById("") 하면 여러개가 있어도 하나의 태그만 리턴되지만,
document.getElementByClassName("") 하면 여러개의 HTMLCollection 이 반환됨.)

### 시맨틱 마크업

특성 목록
특성 이름	요소	설명

<figure class="table-container"><table class="standard-table">
  <thead>
    <tr>
      <th>특성 이름</th>
      <th>요소</th>
      <th>설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>accept</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/form"><code>&lt;form&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a></td>
      <td>서버에서 허용하는 유형의 목록. 보통 파일 유형을 의미합니다.</td>
    </tr>
    <tr>
      <td><code>accept-charset</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/form"><code>&lt;form&gt;</code></a></td>
      <td>지원하는 문자 집합의 목록.</td>
    </tr>
    <tr>
      <td><code>accesskey</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>
        해당 요소로 초점을 이동시키거나 활성화시키기 위한 키보드 단축키를
        정의합니다.
      </td>
    </tr>
    <tr>
      <td><code>action</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/form"><code>&lt;form&gt;</code></a></td>
      <td>폼(form)으로부터 전송된 정보를 처리할 프로그램의 URI입니다.</td>
    </tr>
    <tr>
      <td><code>align</code></td>
      <td>
        <a class="page-not-created" title="이 문서는 아직 작성되지 않았습니다. 기여해 주시겠어요?"><code>&lt;applet&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/caption"><code>&lt;caption&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/col"><code>&lt;col&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/colgroup"><code>&lt;colgroup&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/hr"><code>&lt;hr&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/iframe"><code>&lt;iframe&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/table"><code>&lt;table&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/tbody"><code>&lt;tbody&gt;</code> <small>(en-US)</small></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/td"><code>&lt;td&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/tfoot"><code>&lt;tfoot&gt;</code></a> , <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/th"><code>&lt;th&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/thead"><code>&lt;thead&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/tr"><code>&lt;tr&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>해당 요소의 가로 정렬 방식을 명시합니다.</td>
    </tr>
    <tr>
      <td><code><a href="/ko/docs/Web/HTML/Attributes/allow" class="page-not-created" title="This is a link to an unwritten page">allow</a></code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/iframe"><code>&lt;iframe&gt;</code> <small>(en-US)</small></a></td>
      <td>Specifies a feature-policy for the iframe.</td>
    </tr>
    <tr>
      <td><code>alt</code></td>
      <td>
        <a class="page-not-created" title="이 문서는 아직 작성되지 않았습니다. 기여해 주시겠어요?"><code>&lt;applet&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/area"><code>&lt;area&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>이미지를 표시할 수 없는 경우 표시할 대체 문구입니다.</td>
    </tr>
    <tr>
      <td><code>async</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/script"><code>&lt;script&gt;</code></a></td>
      <td>해당 스크립트는 비동기적으로 실행되어야함을 나타냅니다.</td>
    </tr>
    <tr>
      <td><code>autocapitalize</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>
        사용자가 입력하거나 편집하는 문구를 자동으로 대문자로 바꿀지 여부와
        방법을 제어합니다.
      </td>
    </tr>
    <tr>
      <td><code>autocomplete</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/form"><code>&lt;form&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>
        이 폼 내의 컨트롤에 대해 브라우저가 지원하는 값 자동완성 기능을 기본으로
        설정할 것인지를 나타냅니다.
      </td>
    </tr>
    <tr>
      <td><code>autofocus</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/button"><code>&lt;button&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/select"><code>&lt;select&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>페이지가 로드된 후 자동으로 해당 요소로 초점이 이동합니다.</td>
    </tr>
    <tr>
      <td><code>autoplay</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/audio"><code>&lt;audio&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/video"><code>&lt;video&gt;</code></a>
      </td>
      <td>오디오나 비디오가 가능한 빠른 시점에 재생됩니다.</td>
    </tr>
    <tr>
      <td><code>background</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/body"><code>&lt;body&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/table"><code>&lt;table&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/td"><code>&lt;td&gt;</code> <small>(en-US)</small></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/th"><code>&lt;th&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>Specifies the URL of an image file.
        <div class="note notecard" id="sect1">
          <strong>Note:</strong> Although browsers and email clients may still
          support this attribute, it is obsolete. Use CSS
          <a href="/ko/docs/Web/CSS/background-image"><code>background-image</code></a> instead.
        </div>
      </td>
    </tr>
    <tr>
      <td><code>bgcolor</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/body"><code>&lt;body&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/col"><code>&lt;col&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/colgroup"><code>&lt;colgroup&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/marquee"><code>&lt;marquee&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/table"><code>&lt;table&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/tbody"><code>&lt;tbody&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/tfoot"><code>&lt;tfoot&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/td"><code>&lt;td&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/th"><code>&lt;th&gt;</code> <small>(en-US)</small></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/tr"><code>&lt;tr&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>
        <p>요소의 배경색입니다.</p>
        <div class="note notecard" id="sect2">
          <p>
            <strong>주:</strong> 이 속성은 더 이상 사용하지 않습니다. CSS의
            <a href="/ko/docs/Web/CSS/background-color"><code>background-color</code></a> 속성을 대신 사용하시기
            바랍니다.
          </p>
        </div>
      </td>
    </tr>
    <tr>
      <td><code>border</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/object"><code>&lt;object&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/table"><code>&lt;table&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>
        <p>선의 굵기입니다.</p>
        <div class="note notecard" id="sect3">
          <p>
            <strong>주:</strong> 이 속성은 더 이상 사용하지 않습니다. CSS의
            <a href="/ko/docs/Web/CSS/border"><code>border</code></a> 속성을 대신 사용하시기 바랍니다.
          </p>
        </div>
      </td>
    </tr>
    <tr>
      <td><code>buffered</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/audio"><code>&lt;audio&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/video"><code>&lt;video&gt;</code></a>
      </td>
      <td>이미 버퍼링된 미디어의 시간 범위를 가집니다.</td>
    </tr>
    <tr>
      <td><code><a href="/en-US/docs/Web/HTML/Attributes/capture" class="only-in-en-us" title="Currently only available in English (US)">capture <small>(en-US)<small></small></small></a></code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a></td>
      <td>
        From the
        media capture spec,
        specifies a new file can be captured.
      </td>
    </tr>
    <tr>
      <td><code>charset</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/meta"><code>&lt;meta&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/script"><code>&lt;script&gt;</code></a></td>
      <td>페이지 또는 스크립트의 문자 인코딩을 선언합니다.</td>
    </tr>
    <tr>
      <td><code>checked</code></td>
      <td>
        <a class="page-not-created" title="이 문서는 아직 작성되지 않았습니다. 기여해 주시겠어요?"><code>&lt;command&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>페이지가 로딩될 때, 해당 요소가 체크되어 있어야하는지를 나타냅니다.</td>
    </tr>
    <tr>
      <td><code>cite</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/blockquote"><code>&lt;blockquote&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/del"><code>&lt;del&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/ins"><code>&lt;ins&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/q"><code>&lt;q&gt;</code></a>
      </td>
      <td>변경 또는 인용구문의 출처를 가리키는 URI를 가집니다.</td>
    </tr>
    <tr>
      <td><code>class</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>공통적인 속성으로 요소의 스타일을 지정할 때 CSS와 함께 자주 사용됩니다.</td>
    </tr>
    <tr>
      <td><code>code</code></td>
      <td><a class="page-not-created" title="이 문서는 아직 작성되지 않았습니다. 기여해 주시겠어요?"><code>&lt;applet&gt;</code></a></td>
      <td>로딩 후 실행할 애플릿의 클래스 파일의 URL을 명시합니다.</td>
    </tr>
    <tr>
      <td><code>codebase</code></td>
      <td><a class="page-not-created" title="이 문서는 아직 작성되지 않았습니다. 기여해 주시겠어요?"><code>&lt;applet&gt;</code></a></td>
      <td>
        이 속성은 코드(code) 속성이 참조하는 애플릿의 .class 파일이 저장되어
        있는 디렉토리의 절대경로 또는 상대경로 URL을 제공합니다.
      </td>
    </tr>
    <tr>
      <td><code>color</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/CSS/CSS_fonts"><code>&lt;basefont&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/font"><code>&lt;font&gt;</code> <small>(en-US)</small></a>, <a href="/ko/docs/Web/HTML/Element/hr"><code>&lt;hr&gt;</code></a>
      </td>
      <td>
        <p>
          이 속성은 미리 정의된 색상 명칭 또는 #RRGGBB 형식의 16진수로 명시된
          색상으로 텍스트 색상을 설정한다.
        </p>
        <div class="note notecard" id="sect4">
          <p>
            <strong>주:</strong> 이 속성은 더 이상 사용하지 않습니다. CSS의
            <a href="/ko/docs/Web/CSS/color"><code>color</code></a> 속성을 대신 사용하시기 바랍니다.
          </p>
        </div>
      </td>
    </tr>
    <tr>
      <td><code>cols</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a></td>
      <td>textarea에 표시할 컬럼의 수를 정의한다.</td>
    </tr>
    <tr>
      <td><code>colspan</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/td"><code>&lt;td&gt;</code> <small>(en-US)</small></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/th"><code>&lt;th&gt;</code> <small>(en-US)</small></a></td>
      <td>colspan 속성은 어떤 셀이 확장되어야 할 컬럼의 수를 정의한다.</td>
    </tr>
    <tr>
      <td><code>content</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/meta"><code>&lt;meta&gt;</code></a></td>
      <td>
        A value associated with <code>http-equiv</code> or
        <code>name</code> depending on the context.
      </td>
    </tr>
    <tr>
      <td><code>contenteditable</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>Indicates whether the element's content is editable.</td>
    </tr>
    <tr>
      <td><code>contextmenu</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>
        Defines the ID of a <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/menu"><code>&lt;menu&gt;</code> <small>(en-US)</small></a> element which will
        serve as the element's context menu.
      </td>
    </tr>
    <tr>
      <td><code>controls</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/audio"><code>&lt;audio&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/video"><code>&lt;video&gt;</code></a>
      </td>
      <td>Indicates whether the browser should show playback controls to the user.</td>
    </tr>
    <tr>
      <td><code>coords</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/area"><code>&lt;area&gt;</code></a></td>
      <td>A set of values specifying the coordinates of the hot-spot region.</td>
    </tr>
    <tr>
      <td><code><a href="/en-US/docs/Web/HTML/Attributes/crossorigin" class="only-in-en-us" title="Currently only available in English (US)">crossorigin <small>(en-US)<small></small></small></a></code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/audio"><code>&lt;audio&gt;</code> <small>(en-US)</small></a>, <a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/link"><code>&lt;link&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/script"><code>&lt;script&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/video"><code>&lt;video&gt;</code></a>
      </td>
      <td>How the element handles cross-origin requests</td>
    </tr>
    <tr>
      <td>
        <code><a href="/en-US/docs/Web/API/HTMLIFrameElement/csp" class="only-in-en-us" title="Currently only available in English (US)">csp <small>(en-US)<small></small></small></a></code>
        <abbr class="icon icon-experimental" title="Experimental. 예상되는 동작은 향후 변경될 수 있습니다.">
    <span class="visually-hidden">Experimental</span>
</abbr>
      </td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/iframe"><code>&lt;iframe&gt;</code> <small>(en-US)</small></a></td>
      <td>
        Specifies the Content Security Policy that an embedded document must
        agree to enforce upon itself.
      </td>
    </tr>
    <tr>
      <td><code>data</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/object"><code>&lt;object&gt;</code></a></td>
      <td>Specifies the URL of the resource.</td>
    </tr>
    <tr>
      <td><code>data-*</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>Lets you attach custom attributes to an HTML element.</td>
    </tr>
    <tr>
      <td><code>datetime</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/del"><code>&lt;del&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/ins"><code>&lt;ins&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/time"><code>&lt;time&gt;</code></a>
      </td>
      <td>Indicates the date and time associated with the element.</td>
    </tr>
    <tr>
      <td><code><a href="/ko/docs/Web/HTML/Attributes/decoding" class="page-not-created" title="This is a link to an unwritten page">decoding</a></code></td>
      <td><a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a></td>
      <td>Indicates the preferred method to decode the image.</td>
    </tr>
    <tr>
      <td><code>default</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/track"><code>&lt;track&gt;</code></a></td>
      <td>
        Indicates that the track should be enabled unless the user's preferences
        indicate something different.
      </td>
    </tr>
    <tr>
      <td><code>defer</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/script"><code>&lt;script&gt;</code></a></td>
      <td>
        Indicates that the script should be executed after the page has been
        parsed.
      </td>
    </tr>
    <tr>
      <td><code>dir</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>
        Defines the text direction. Allowed values are ltr (Left-To-Right) or
        rtl (Right-To-Left)
      </td>
    </tr>
    <tr>
      <td><code>dirname</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>
      </td>
      <td></td>
    </tr>
    <tr>
      <td><code>disabled</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/button"><code>&lt;button&gt;</code></a>,
        <a class="page-not-created" title="이 문서는 아직 작성되지 않았습니다. 기여해 주시겠어요?"><code>&lt;command&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/fieldset"><code>&lt;fieldset&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/optgroup"><code>&lt;optgroup&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/option"><code>&lt;option&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/select"><code>&lt;select&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>Indicates whether the user can interact with the element.</td>
    </tr>
    <tr>
      <td><code>download</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/a"><code>&lt;a&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/area"><code>&lt;area&gt;</code></a></td>
      <td>Indicates that the hyperlink is to be used for downloading a resource.</td>
    </tr>
    <tr>
      <td><code>draggable</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>Defines whether the element can be dragged.</td>
    </tr>
    <tr>
      <td><code>dropzone</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>Indicates that the element accept the dropping of content on it.</td>
    </tr>
    <tr>
      <td><code>enctype</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/form"><code>&lt;form&gt;</code></a></td>
      <td>
        Defines the content type of the form date when the
        <code>method</code> is POST.
      </td>
    </tr>
    <tr>
      <td>
        <code><a href="/ko/docs/Web/HTML/Attributes/enterkeyhint" class="page-not-created" title="This is a link to an unwritten page">enterkeyhint</a></code>
        <abbr class="icon icon-experimental" title="Experimental. 예상되는 동작은 향후 변경될 수 있습니다.">
    <span class="visually-hidden">Experimental</span>
</abbr>
      </td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Global_attributes/contenteditable"><code>contenteditable</code></a>
      </td>
      <td>
        The
        <a href="https://html.spec.whatwg.org/dev/interaction.html#input-modalities:-the-enterkeyhint-attribute" class="external" target="_blank"><code>enterkeyhint</code></a>
        specifies what action label (or icon) to present for the enter key on
        virtual keyboards. The attribute can be used with form controls (such as
        the value of <code>textarea</code> elements), or in elements in an
        editing host (e.g., using <code>contenteditable</code> attribute).
      </td>
    </tr>
    <tr>
      <td><code>for</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/label"><code>&lt;label&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/output"><code>&lt;output&gt;</code></a>
      </td>
      <td>Describes elements which belongs to this one.</td>
    </tr>
    <tr>
      <td><code>form</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/button"><code>&lt;button&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/fieldset"><code>&lt;fieldset&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/label"><code>&lt;label&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/meter"><code>&lt;meter&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/object"><code>&lt;object&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/output"><code>&lt;output&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/progress"><code>&lt;progress&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/select"><code>&lt;select&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>Indicates the form that is the owner of the element.</td>
    </tr>
    <tr>
      <td><code>formaction</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/button"><code>&lt;button&gt;</code></a>
      </td>
      <td>
        Indicates the action of the element, overriding the action defined in
        the <a href="/ko/docs/Web/HTML/Element/form"><code>&lt;form&gt;</code></a>.
      </td>
    </tr>
    <tr>
      <td><code><a href="/ko/docs/Web/HTML/Attributes/formenctype" class="page-not-created" title="This is a link to an unwritten page">formenctype</a></code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/button"><code>&lt;button&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>
        If the button/input is a submit button (<code>type="submit"</code>),
        this attribute sets the encoding type to use during form submission. If
        this attribute is specified, it overrides the
        <code>enctype</code> attribute of the button's
        <a href="/ko/docs/Web/HTML/Element/form">form</a> owner.
      </td>
    </tr>
    <tr>
      <td><code><a href="/ko/docs/Web/HTML/Attributes/formmethod" class="page-not-created" title="This is a link to an unwritten page">formmethod</a></code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/button"><code>&lt;button&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>
        If the button/input is a submit button (<code>type="submit"</code>),
        this attribute sets the submission method to use during form submission
        (<code>GET</code>, <code>POST</code>, etc.). If this attribute is
        specified, it overrides the <code>method</code> attribute of the
        button's <a href="/ko/docs/Web/HTML/Element/form">form</a> owner.
      </td>
    </tr>
    <tr>
      <td><code><a href="/ko/docs/Web/HTML/Attributes/formnovalidate" class="page-not-created" title="This is a link to an unwritten page">formnovalidate</a></code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/button"><code>&lt;button&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>
        If the button/input is a submit button (<code>type="submit"</code>),
        this boolean attribute specifies that the form is not to be validated
        when it is submitted. If this attribute is specified, it overrides the
        <code>novalidate</code> attribute of the button's
        <a href="/ko/docs/Web/HTML/Element/form">form</a> owner.
      </td>
    </tr>
    <tr>
      <td><code><a href="/ko/docs/Web/HTML/Attributes/formtarget" class="page-not-created" title="This is a link to an unwritten page">formtarget</a></code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/button"><code>&lt;button&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>
        If the button/input is a submit button (<code>type="submit"</code>),
        this attribute specifies the browsing context (for example, tab, window,
        or inline frame) in which to display the response that is received after
        submitting the form. If this attribute is specified, it overrides the
        <code>target</code> attribute of the button's
        <a href="/ko/docs/Web/HTML/Element/form">form</a> owner.
      </td>
    </tr>
    <tr>
      <td><code>headers</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/td"><code>&lt;td&gt;</code> <small>(en-US)</small></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/th"><code>&lt;th&gt;</code> <small>(en-US)</small></a></td>
      <td>
        IDs of the <code>&lt;th&gt;</code> elements which applies to this
        element.
      </td>
    </tr>
    <tr>
      <td><code>height</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/canvas"><code>&lt;canvas&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/embed"><code>&lt;embed&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/iframe"><code>&lt;iframe&gt;</code> <small>(en-US)</small></a>, <a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/object"><code>&lt;object&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/video"><code>&lt;video&gt;</code></a>
      </td>
      <td>
        <p>
          Specifies the height of elements listed here. For all other elements,
          use the CSS <a href="/ko/docs/Web/CSS/height"><code>height</code></a> property.
        </p>
        <div class="note notecard" id="sect5">
          <p>
            <strong>Note:</strong> In some instances, such as
            <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/div"><code>&lt;div&gt;</code> <small>(en-US)</small></a>, this is a legacy attribute, in
            which case the CSS <a href="/ko/docs/Web/CSS/height"><code>height</code></a> property should
            be used instead.
          </p>
        </div>
      </td>
    </tr>
    <tr></tr>
    <tr>
      <td><code>hidden</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>
        Prevents rendering of given element, while keeping child elements, e.g.
        script elements, active.
      </td>
    </tr>
    <tr>
      <td><code>high</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/meter"><code>&lt;meter&gt;</code></a></td>
      <td>Indicates the lower bound of the upper range.</td>
    </tr>
    <tr>
      <td><code>href</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/a"><code>&lt;a&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/area"><code>&lt;area&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/base"><code>&lt;base&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/link"><code>&lt;link&gt;</code></a>
      </td>
      <td>링크된 리소스의 URL</td>
    </tr>
    <tr>
      <td><code>hreflang</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/a"><code>&lt;a&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/area"><code>&lt;area&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/link"><code>&lt;link&gt;</code></a>
      </td>
      <td>링크된 리소스의 언어를 나타냄</td>
    </tr>
    <tr>
      <td><code>http-equiv</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/meta"><code>&lt;meta&gt;</code></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>icon</code></td>
      <td><a class="page-not-created" title="이 문서는 아직 작성되지 않았습니다. 기여해 주시겠어요?"><code>&lt;command&gt;</code></a></td>
      <td>Specifies a picture which represents the command.</td>
    </tr>
    <tr>
      <td><code>id</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>
        일반적으로, 특정한 요소를 스타일하기 위해 CSS와 함꼐 사용됨. 이 속성의
        값은 유일해야함.
      </td>
    </tr>
    <tr>
      <td>
        <code><a href="/ko/docs/Web/HTML/Attributes/importance" class="page-not-created" title="This is a link to an unwritten page">importance</a></code>
        <abbr class="icon icon-experimental" title="Experimental. 예상되는 동작은 향후 변경될 수 있습니다.">
    <span class="visually-hidden">Experimental</span>
</abbr>
      </td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/iframe"><code>&lt;iframe&gt;</code> <small>(en-US)</small></a>, <a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/link"><code>&lt;link&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/script"><code>&lt;script&gt;</code></a>
      </td>
      <td>Indicates the relative fetch priority for the resource.</td>
    </tr>
    <tr>
      <td><code><a href="/ko/docs/Web/Security/Subresource_Integrity">integrity</a></code></td>
      <td><a href="/ko/docs/Web/HTML/Element/link"><code>&lt;link&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/script"><code>&lt;script&gt;</code></a></td>
      <td>
        Specifies a
        <a href="/ko/docs/Web/Security/Subresource_Integrity">Subresource Integrity</a>
        value that allows browsers to verify what they fetch.
      </td>
    </tr>
    <tr>
      <td>
        <a href="/ko/docs/Web/HTML/Element/img#intrinsicsize"><code>intrinsicsize</code></a>
        <abbr class="icon icon-deprecated" title="지원이 중단되었습니다. 새로운 웹사이트에서 사용하지 마세요.">
  <span class="visually-hidden">지원이 중단되었습니다</span>
</abbr>
      </td>
      <td><a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a></td>
      <td>
        This attribute tells the browser to ignore the actual intrinsic size of
        the image and pretend it's the size specified in the attribute.
      </td>
    </tr>
    <tr>
      <td><a href="/ko/docs/Web/HTML/Global_attributes/inputmode"><code>inputmode</code></a></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Global_attributes/contenteditable"><code>contenteditable</code></a>
      </td>
      <td>
        Provides a hint as to the type of data that might be entered by the user
        while editing the element or its contents. The attribute can be used
        with form controls (such as the value of
        <code>textarea</code> elements), or in elements in an editing host
        (e.g., using <code>contenteditable</code> attribute).
      </td>
    </tr>
    <tr>
      <td><code>ismap</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a></td>
      <td>Indicates that the image is part of a server-side image map.</td>
    </tr>
    <tr>
      <td><code>itemprop</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>kind</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/track"><code>&lt;track&gt;</code></a></td>
      <td>Specifies the kind of text track.</td>
    </tr>
    <tr>
      <td><code>label</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/track"><code>&lt;track&gt;</code></a></td>
      <td>Specifies a user-readable title of the text track.</td>
    </tr>
    <tr>
      <td><code>lang</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>요소에서 사용된 언어를 정의합니다.</td>
    </tr>
    <tr>
      <td><code>language</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/script"><code>&lt;script&gt;</code></a></td>
      <td>요소에서 사용된 스크립트 언어를 정의합니다.</td>
    </tr>
    <tr>
      <td><code>list</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a></td>
      <td>Identifies a list of pre-defined options to suggest to the user.</td>
    </tr>
    <tr>
      <td><code>loading</code> <abbr class="icon icon-experimental" title="Experimental. 예상되는 동작은 향후 변경될 수 있습니다.">
    <span class="visually-hidden">Experimental</span>
</abbr></td>
      <td><a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/iframe"><code>&lt;iframe&gt;</code> <small>(en-US)</small></a></td>
      <td>
        Indicates if the element should be loaded lazily
        (<code>loading="lazy"</code>) or loaded immediately
        (<code>loading="eager"</code>).
      </td>
    </tr>
    <tr>
      <td><code><a href="/ko/docs/Web/HTML/Attributes/list" class="page-not-created" title="This is a link to an unwritten page">list</a></code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a></td>
      <td>Identifies a list of pre-defined options to suggest to the user.</td>
    </tr>
    <tr>
      <td><code>loop</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/audio"><code>&lt;audio&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/audio"><code>&lt;bgsound&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/marquee"><code>&lt;marquee&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/video"><code>&lt;video&gt;</code></a>
      </td>
      <td>미디어가 재생을 완료했을때 다시 재생을 시작해야할지를 나타냅니다.</td>
    </tr>
    <tr>
      <td><code>low</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/meter"><code>&lt;meter&gt;</code></a></td>
      <td>Indicates the upper bound of the lower range.</td>
    </tr>
    <tr>
      <td><code>manifest</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/html"><code>&lt;html&gt;</code></a></td>
      <td>문서의 캐시 매니페스트의 URL을 가리킵니다.</td>
    </tr>
    <tr>
      <td><code>max</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/meter"><code>&lt;meter&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/progress"><code>&lt;progress&gt;</code></a>
      </td>
      <td>허용되는 최대 값을 나타냅니다.</td>
    </tr>
    <tr>
      <td><code>maxlength</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>요소에 허용되는 문자의 최대 길이를 나타냅니다.</td>
    </tr>
    <tr>
      <td><code><a href="/en-US/docs/Web/HTML/Attributes/minlength" class="only-in-en-us" title="Currently only available in English (US)">minlength <small>(en-US)<small></small></small></a></code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>Defines the minimum number of characters allowed in the element.</td>
    </tr>
    <tr>
      <td><code>media</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/a"><code>&lt;a&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/area"><code>&lt;area&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/link"><code>&lt;link&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/source"><code>&lt;source&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/style"><code>&lt;style&gt;</code></a>
      </td>
      <td>
        Specifies a hint of the media for which the linked resource was
        designed.
      </td>
    </tr>
    <tr>
      <td><code>method</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/form"><code>&lt;form&gt;</code></a></td>
      <td>
        폼을 제출할때 사용할 HTTP 메소드를 정의함. GET(기본값) 또는 POST 가 될수
        있음.
      </td>
    </tr>
    <tr>
      <td><code>min</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/meter"><code>&lt;meter&gt;</code></a>
      </td>
      <td>허용되는 최소 값을 나타냄.</td>
    </tr>
    <tr>
      <td><code>multiple</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/select"><code>&lt;select&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>
        Indicates whether multiple values can be entered in an input of the type
        <code>email</code> or <code>file</code>.
      </td>
    </tr>
    <tr>
      <td><code><a href="/ko/docs/Web/HTML/Attributes/muted" class="page-not-created" title="This is a link to an unwritten page">muted</a></code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/audio"><code>&lt;audio&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/video"><code>&lt;video&gt;</code></a>
      </td>
      <td>Indicates whether the audio will be initially silenced on page load.</td>
    </tr>
    <tr>
      <td><code>name</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/button"><code>&lt;button&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/form"><code>&lt;form&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/fieldset"><code>&lt;fieldset&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/iframe"><code>&lt;iframe&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/object"><code>&lt;object&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/output"><code>&lt;output&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/select"><code>&lt;select&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/map"><code>&lt;map&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/meta"><code>&lt;meta&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/param"><code>&lt;param&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>
        요소의 이름. For example used by the server to identify the fields in
        form submits.
      </td>
    </tr>
    <tr>
      <td><code>novalidate</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/form"><code>&lt;form&gt;</code></a></td>
      <td>
        This attribute indicates that the form shouldn't be validated when
        submitted.
      </td>
    </tr>
    <tr>
      <td><code>open</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/details"><code>&lt;details&gt;</code> <small>(en-US)</small></a></td>
      <td>Indicates whether the details will be shown on page load.</td>
    </tr>
    <tr>
      <td><code>optimum</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/meter"><code>&lt;meter&gt;</code></a></td>
      <td>Indicates the optimal numeric value.</td>
    </tr>
    <tr>
      <td><code>pattern</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a></td>
      <td>
        Defines a regular expression which the element's value will be validated
        against.
      </td>
    </tr>
    <tr>
      <td><code>ping</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/a"><code>&lt;a&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/area"><code>&lt;area&gt;</code></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>placeholder</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>필드에 무엇이 들어갈수 있는지 사용자에게 힌트를 제공합니다.</td>
    </tr>
    <tr>
      <td><code>poster</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/video"><code>&lt;video&gt;</code></a></td>
      <td>A URL indicating a poster frame to show until the user plays or seeks.</td>
    </tr>
    <tr>
      <td><code>preload</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/audio"><code>&lt;audio&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/video"><code>&lt;video&gt;</code></a>
      </td>
      <td>전체,부분,또는 아무런 리소스가 미리 로드되어야하는지를 나타냅니다.</td>
    </tr>
    <tr>
      <td><code>radiogroup</code></td>
      <td><a class="page-not-created" title="이 문서는 아직 작성되지 않았습니다. 기여해 주시겠어요?"><code>&lt;command&gt;</code></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>readonly</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>요소가 수정될 수 있는지를 나타냅니다.</td>
    </tr>
    <tr>
      <td><code>rel</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/a"><code>&lt;a&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/area"><code>&lt;area&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/link"><code>&lt;link&gt;</code></a>
      </td>
      <td>Specifies the relationship of the target object to the link object.</td>
    </tr>
    <tr>
      <td><code>required</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/select"><code>&lt;select&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>이 요소가 채워져야 하는지를 나타냅니다.</td>
    </tr>
    <tr>
      <td><code>reversed</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/ol"><code>&lt;ol&gt;</code></a></td>
      <td>
        Indicates whether the list should be displayed in a descending order
        instead of a ascending.
      </td>
    </tr>
    <tr>
      <td><code>rows</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a></td>
      <td>textarea의 줄 개수를 정의합니다.</td>
    </tr>
    <tr>
      <td><code>rowspan</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/td"><code>&lt;td&gt;</code> <small>(en-US)</small></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/th"><code>&lt;th&gt;</code> <small>(en-US)</small></a></td>
      <td>Defines the number of rows a table cell should span over.</td>
    </tr>
    <tr>
      <td><code>sandbox</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/iframe"><code>&lt;iframe&gt;</code> <small>(en-US)</small></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>scope</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/th"><code>&lt;th&gt;</code> <small>(en-US)</small></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>scoped</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/style"><code>&lt;style&gt;</code></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>selected</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/option"><code>&lt;option&gt;</code></a></td>
      <td>Defines a value which will be selected on page load.</td>
    </tr>
    <tr>
      <td><code>shape</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/a"><code>&lt;a&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/area"><code>&lt;area&gt;</code></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>size</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/select"><code>&lt;select&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>
        Defines the width of the element (in pixels). If the element's
        <code>type</code> attribute is <code>text</code> or
        <code>password</code> then it's the number of characters.
      </td>
    </tr>
    <tr>
      <td><code>sizes</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/link"><code>&lt;link&gt;</code></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>slot</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>Assigns a slot in a shadow DOM shadow tree to an element.</td>
    </tr>
    <tr>
      <td><code>span</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/col"><code>&lt;col&gt;</code> <small>(en-US)</small></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/colgroup"><code>&lt;colgroup&gt;</code> <small>(en-US)</small></a>
      </td>
      <td></td>
    </tr>
    <tr>
      <td><code><a href="/ko/docs/Web/HTML/Attributes/spellcheck" class="page-not-created" title="This is a link to an unwritten page">spellcheck</a></code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>Indicates whether spell checking is allowed for the element.</td>
    </tr>
    <tr>
      <td><code>src</code></td>
      <td>
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/audio"><code>&lt;audio&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/embed"><code>&lt;embed&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/iframe"><code>&lt;iframe&gt;</code> <small>(en-US)</small></a>, <a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/script"><code>&lt;script&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/source"><code>&lt;source&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/track"><code>&lt;track&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/video"><code>&lt;video&gt;</code></a>
      </td>
      <td>내장 컨텐츠의 URL</td>
    </tr>
    <tr>
      <td><code>srcdoc</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/iframe"><code>&lt;iframe&gt;</code> <small>(en-US)</small></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>srclang</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/track"><code>&lt;track&gt;</code></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>srcset</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>start</code></td>
      <td><a href="/ko/docs/Web/HTML/Element/ol"><code>&lt;ol&gt;</code></a></td>
      <td>Defines the first number if other than 1.</td>
    </tr>
    <tr>
      <td><code>step</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>style</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>이전 스타일을 오버라이드할 CSS 스타일을 정의함.</td>
    </tr>
    <tr>
      <td><code>summary</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/table"><code>&lt;table&gt;</code> <small>(en-US)</small></a></td>
      <td></td>
    </tr>
    <tr>
      <td><code>tabindex</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>
        Overrides the browser's default tab order and follows the one specified
        instead.
      </td>
    </tr>
    <tr>
      <td><code>target</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/a"><code>&lt;a&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/area"><code>&lt;area&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/base"><code>&lt;base&gt;</code></a>, <a href="/ko/docs/Web/HTML/Element/form"><code>&lt;form&gt;</code></a>
      </td>
      <td></td>
    </tr>
    <tr>
      <td><code>title</code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>요소 위에 호버링했을떄 표시될 툴팁의 텍스트</td>
    </tr>
    <tr>
      <td><code><a href="/ko/docs/Web/HTML/Attributes/translate" class="page-not-created" title="This is a link to an unwritten page">translate</a></code></td>
      <td><a href="/ko/docs/Web/HTML/Global_attributes">전역 특성</a></td>
      <td>
        Specify whether an element's attribute values and the values of its
        <code><a href="https://dom.spec.whatwg.org/#text" id="ref-for-text①⑦" class="external" target="_blank">Text</a></code>
        node children are to be translated when the page is localized, or
        whether to leave them unchanged.
      </td>
    </tr>
    <tr>
      <td><code>type</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/button"><code>&lt;button&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a class="page-not-created" title="이 문서는 아직 작성되지 않았습니다. 기여해 주시겠어요?"><code>&lt;command&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/embed"><code>&lt;embed&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/object"><code>&lt;object&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/script"><code>&lt;script&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/source"><code>&lt;source&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/style"><code>&lt;style&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/menu"><code>&lt;menu&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>요소의 타입을 정의함</td>
    </tr>
    <tr>
      <td><code>usemap</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a>, <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/object"><code>&lt;object&gt;</code></a>
      </td>
      <td></td>
    </tr>
    <tr>
      <td><code>value</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/button"><code>&lt;button&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/option"><code>&lt;option&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>, <a href="/ko/docs/Web/HTML/Element/li"><code>&lt;li&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/meter"><code>&lt;meter&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/progress"><code>&lt;progress&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/param"><code>&lt;param&gt;</code> <small>(en-US)</small></a>
      </td>
      <td>페이지가 로드된뒤 요소에 표시될 기본값을 지정합니다.</td>
    </tr>
    <tr>
      <td><code>width</code></td>
      <td>
        <a href="/ko/docs/Web/HTML/Element/canvas"><code>&lt;canvas&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/embed"><code>&lt;embed&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/iframe"><code>&lt;iframe&gt;</code> <small>(en-US)</small></a>, <a href="/ko/docs/Web/HTML/Element/img"><code>&lt;img&gt;</code></a>,
        <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/input"><code>&lt;input&gt;</code> <small>(en-US)</small></a>,
        <a href="/ko/docs/Web/HTML/Element/object"><code>&lt;object&gt;</code></a>,
        <a href="/ko/docs/Web/HTML/Element/video"><code>&lt;video&gt;</code></a>
      </td>
      <td>
        Note: In some instances, such as <a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/div"><code>&lt;div&gt;</code> <small>(en-US)</small></a>, this
        is a legacy attribute, in which case the CSS
        <a href="/ko/docs/Web/CSS/width"><code>width</code></a> property should be used instead. In other
        cases, such as <a href="/ko/docs/Web/HTML/Element/canvas"><code>&lt;canvas&gt;</code></a>, the width must be
        specified with this attribute.
      </td>
    </tr>
    <tr>
      <td><code>wrap</code></td>
      <td><a class="only-in-en-us" title="Currently only available in English (US)" href="/en-US/docs/Web/HTML/Element/textarea"><code>&lt;textarea&gt;</code> <small>(en-US)</small></a></td>
      <td>Indicates whether the text should be wrapped.</td>
    </tr>
  </tbody>
</table></figure>
