### Context
프로그램에서 날씨 정보를 필요로 할 때, 무료 API를 활용하여 손쉽게 데이터를 가져올 수 있다. wttr.in은 curl이나 프로그래밍 언어로 간편하게 접근할 수 있는 날씨 서비스이다.

### Core
```python
import requests

def get_weather(city):
    """
    wttr.in API를 사용해 특정 도시의 날씨 정보를 JSON 형식으로 조회한다.
    """
    url = f"https://wttr.in/{city}?format=j1"
    try:
        response = requests.get(url)
        response.raise_for_status()
        data = response.json()
        return data
    except requests.exceptions.RequestException as e:
        print(f"Error fetching weather: {e}")
        return None

# 서울 날씨 조회 예제
seoul_weather = get_weather("Seoul")
if seoul_weather:
    print(seoul_weather)
```

### Insight
실행 시 반환되는 JSON 객체는 리스트이며, 첫 번째 요소(`[0]`)에 날씨 정보가 포함된다. 주요 키로는 `temp_C`(섭씨 온도), `FeelsLikeC`(체감온도), `humidity`(습도), `windspeedKmph`(풍속), `weatherDesc`(날씨 설명) 등이 있다. `wttr.in`은 기본 텍스트/ASCII 아트 형식 외에도 `format=j1` 파라미터로 JSON 출력을 지원한다. 별도의 API 키 없이 무료로 사용 가능하나, 상업적 목적이나 과도한 호출 시 제한이 있을 수 있으니 공식 문서를 참고해 적절히 활용해야 한다.

**출처:** [wttr.in — The Web Frontend for the console based weather forecast program "WEATHER"](https://wttr.in)