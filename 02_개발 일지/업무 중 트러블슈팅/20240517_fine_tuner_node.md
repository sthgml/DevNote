# Fine Tuner 노드 및 패널

## UI WireFrame

![UI WireFrame](/99_images/240519_fine_tuner/fine_tuner_wireframe.png);

## Layout 퍼블리싱

![alt text](/99_images/240519_fine_tuner/fine_tuner_publishing.png)

## 기존 Interactive annotation 이식하기

![alt text](/99_images/240519_fine_tuner/fine_tuner_annotation.png)
![alt text](/99_images/240519_fine_tuner/fine_tuner_transplant.png)

## mockData로 state 및 props 연결

![alt text](/99_images/240519_fine_tuner/fine_tuner_data.png)
![alt text](/99_images/240519_fine_tuner/fine_tuner_data2.png)

## test api 연결

![alt text](/99_images/240519_fine_tuner/fine_tuner_test_api.png)

```tsx
 console.log(`
    (노드 아이디) key: ${initOption.current.nodeId}, 
    (사용자 입력 값) correction_key: ${initOption.current.newWeightName} 
    t_model_path : /cloud/member/${user.email}/MLOps/model/${initOption.current.modelName}.py
    t_image_path: ${input0+"/"+imageKey}
    (사용자 선택값 = selectedTrainedWeight) base_weight: ${initOption.current.selectedTrainedWeight} 
  `)
      
 var data = {
    "image_path":t_image_path,
    "model_path":t_model_path,
    "base_weight":t_weight,
    "foreground":annotationData['foreground'],
    "background":annotationData['background'],
  };
  
  var response = await t_api.post(
    "/mlops_finetuning/add_correction/" + t_node_id + "/" + t_correction_key , data
  );
```

## 현재 상태

![alt text](/99_images/240519_fine_tuner/fine_tuner_test_api2.png)
