# CapStone Project

네이버 지도 API를 활용한 Q&A 기반 경로 추천 시스템

## 개발 목표

사용자 질문(Q&A)을 기반으로 추천 경로 및 위치를 제공하는 지능형 지도 서비스 구현.

## 주요기능

- 지도 유형 선택(일반, 위성, 하이브리드 등)
- 출발지와 도착지 간 경로 탐색 및 시각화
- 실시간 교통 정보 활성화/비활성화
- Q&A 시스템(Open API 기반)

# 사용 기술 스택

1.프론트엔드
- HTML ![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
- JavaScript ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
- CSS ![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white)

2.지도 API
- 네이버 지도 API
  
3.외부 API
- Google Places API
- OpenAI GPT API ![ChatGPT](https://img.shields.io/badge/chatGPT-74aa9c?style=for-the-badge&logo=openai&logoColor=white)

## 주요코드
```javascript
function getCoordinatesFromGooglePlaces(query, callback) {
    const googleApiKey = "";

    const url = `https://maps.googleapis.com/maps/api/place/findplacefromtext/json?input=${encodeURIComponent(query)}&inputtype=textquery&fields=geometry&key=${googleApiKey}`;

    console.log("Google Places API 호출 URL:", url);

    fetch(url)
      .then((response) => {
        console.log("Google Places API 응답 상태 코드:", response.status);
        if (!response.ok) {
          throw new Error(`Google Places API 호출 실패 - 상태 코드: ${response.status}`);
        }
        return response.json();
      })
      .then((data) => {
        console.log("Google Places API 응답 데이터:", data);
        if (data.candidates && data.candidates.length > 0) {
          const location = data.candidates[0].geometry.location;
          callback({ lat: location.lat, lng: location.lng });
        } else {
          console.error("Google Places API에서 장소를 찾지 못했습니다.");
          callback(null);
        }
      })
      .catch((error) => {
        console.error("Google Places API 호출 실패:", error);
        callback(null);
      });
  }





