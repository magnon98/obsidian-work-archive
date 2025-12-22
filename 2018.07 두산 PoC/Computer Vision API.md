Computer Vision API  
이 API 키는 현재 활성 상태입니다.
 
7일 남음
 
이미지에서 실용적인 정보를 추출
 
5,000개의 트랜잭션, 분당 20개.
 
끝점  
[https://westcentralus.api.cognitive.microsoft.com/vision/v1.0](https://westcentralus.api.cognitive.microsoft.com/vision/v1.0)
 
[https://westcentralus.api.cognitive.microsoft.com/vision/v2.0](https://westcentralus.api.cognitive.microsoft.com/vision/v2.0)
 
키 1: 7794a0713140454587e6ee1b9efe6b70
 
키 2: 79429129023f42c6a30c4aac15ce4704
      

curl -H "Ocp-Apim-Subscription-Key: 79429129023f42c6a30c4aac15ce4704" \  
-H "Content-Type: application/json" \  
"[https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Categories,Faces,Description&details=Landmarks&language=en](https://westcentralus.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Categories,Faces,Description&details=Landmarks&language=en)" \  
-d '{"url":"http://upload.wikimedia.org/wikipedia/commons/3/3c/Shaki_waterfall.jpg"}'
         

[http://doosan-api.51.15.56.81.nip.io/fuse/azure/vision/v2.0/analyze?visualFeatures=Categories,Faces,Description&details=Landmarks&language=en](http://doosan-api.51.15.56.81.nip.io/fuse/azure/vision/v2.0/analyze?visualFeatures=Categories,Faces,Description&details=Landmarks&language=en)
    
Face  
이 API 키는 현재 활성 상태입니다.
 
7일 남음
 
사진에서 얼굴을 감지, 식별, 분석, 구성 및 태그 지정
 
30,000개의 트랜잭션, 분당 20개.
 
끝점: [https://westcentralus.api.cognitive.microsoft.com/face/v1.0](https://westcentralus.api.cognitive.microsoft.com/face/v1.0)
 
키 1: 90a5632e6c9842b897b71eec6a8f89b2
 
키 2: 03848644851b4fb99b5396a954c8dc7b
   

curl -H "Ocp-Apim-Subscription-Key: 90a5632e6c9842b897b71eec6a8f89b2" \  
-H "Content-Type: application/json" \  
"[https://westcentralus.api.cognitive.microsoft.com/face/v1.0/detect?returnFaceId=true&returnFaceLandmarks=false&returnFaceAttributes=age,gender,headPose,smile,facialHair,glasses,emotion,hair,makeup,occlusion,accessories,blur,exposure,noise](https://westcentralus.api.cognitive.microsoft.com/face/v1.0/detect?returnFaceId=true&returnFaceLandmarks=false&returnFaceAttributes=age,gender,headPose,smile,facialHair,glasses,emotion,hair,makeup,occlusion,accessories,blur,exposure,noise)" \  
-d '{"url":"https://ichef.bbci.co.uk/images/ic/720x405/p06f0c5p.jpg"}'
 
[  
{  
"faceId": "6d08c0a9-6675-4b2b-b7dd-12e96bc24a3d",  
"faceRectangle": {  
"top": 89,  
"left": 289,  
"width": 125,  
"height": 125  
},  
"faceAttributes": {  
"smile": 0.001,  
"headPose": {  
"pitch": 0.0,  
"roll": -16.8,  
"yaw": -23.4  
},  
"gender": "male",  
"age": 57.0,  
"facialHair": {  
"moustache": 0.1,  
"beard": 0.1,  
"sideburns": 0.1  
},  
"glasses": "NoGlasses",  
"emotion": {  
"anger": 0.011,  
"contempt": 0.003,  
"disgust": 0.001,  
"fear": 0.001,  
"happiness": 0.001,  
"neutral": 0.973,  
"sadness": 0.003,  
"surprise": 0.008  
},  
"blur": {  
"blurLevel": "low",  
"value": 0.0  
},  
"exposure": {  
"exposureLevel": "goodExposure",  
"value": 0.59  
},  
"noise": {  
"noiseLevel": "low",  
"value": 0.0  
},  
"makeup": {  
"eyeMakeup": false,  
"lipMakeup": false  
},  
"accessories": [],  
"occlusion": {  
"foreheadOccluded": false,  
"eyeOccluded": false,  
"mouthOccluded": false  
},  
"hair": {  
"bald": 0.61,  
"invisible": false,  
"hairColor": [  
{  
"color": "gray",  
"confidence": 1.0  
},  
{  
"color": "black",  
"confidence": 0.98  
},  
{  
"color": "other",  
"confidence": 0.73  
},  
{  
"color": "blond",  
"confidence": 0.11  
},  
{  
"color": "brown",  
"confidence": 0.05  
},  
{  
"color": "red",  
"confidence": 0.0  
}  
]  
}  
}  
}  
]