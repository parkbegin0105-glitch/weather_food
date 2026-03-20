import requests
from datetime import datetime, timedelta

def get_2day_food_plan(city_name, api_key):
    # 5일 예보 API (오늘과 내일 데이터를 모두 포함함)
    url = f"http://api.openweathermap.org/data/2.5/forecast?q={city_name}&appid={api_key}&units=metric&lang=kr"
    
    try:
        response = requests.get(url).json()
        if response["cod"] != "200": return "도시 정보를 확인해주세요."

        # 1. 데이터 추출 (오늘 현재 vs 내일 이 시간)
        today_data = response['list'][0]   # 현재 시점
        tomorrow_data = response['list'][8] # 약 24시간 뒤 (3시간 * 8)

        def analyze_and_pick(data):
            t = data['main']['temp']
            h = data['main']['humidity']
            w = data['weather'][0]['main']
            
            # 구체적인 추천 로직
            if "Rain" in w or h > 75:
                return {"menu": "바삭한 감자전과 비빔국수", "point": "습한 날씨를 날려줄 바삭함과 매콤함", "drink": "막걸리 또는 탄산수"}
            elif t >= 25:
                return {"menu": "시원한 냉샤브샤브", "point": "낮은 온도로 즐기는 담백한 단백질", "drink": "차가운 녹차"}
            elif t <= 10:
                return {"menu": "진한 사골 떡만둣국", "point": "쌀쌀한 기운을 덮어주는 뜨끈한 육수", "drink": "보리차"}
            elif "Clear" in w:
                return {"menu": "바질 페스토 파스타와 스테이크", "point": "화창한 날씨에 어울리는 향긋하고 고급스러운 풍미", "drink": "화이트 와인 또는 에이드"}
            else:
                return {"menu": "직화 제육쌈밥", "point": "적당한 구름 아래 입맛을 돋우는 불맛", "drink": "쌈채소와 숭늉"}

        today_rec = analyze_and_pick(today_data)
        tomorrow_rec = analyze_and_pick(tomorrow_data)

        # 2. 결과 출력
        print(f"🗓️ [ {city_name} 1박 2일 미식 가이드 ]")
        print("="*55)
        
        # 오늘 출력
        print(f"▶ TODAY (현재: {today_data['weather'][0]['description']}, {today_data['main']['temp']}°C)")
        print(f"   🍴 추천: {today_rec['menu']}")
        print(f"   ✨ 특징: {today_rec['point']}")
        print(f"   🥤 조합: {today_rec['drink']}")
        print("-" * 55)

        # 내일 출력
        tomorrow_date = (datetime.now() + timedelta(days=1)).strftime('%m월 %d일')
        print(f"▶ TOMORROW ({tomorrow_date} 예보: {tomorrow_data['weather'][0]['description']}, {tomorrow_data['main']['temp']}°C)")
        print(f"   🍴 추천: {tomorrow_rec['menu']}")
        print(f"   ✨ 특징: {tomorrow_rec['point']}")
        print(f"   🥤 조합: {tomorrow_rec['drink']}")
        print("="*55)

    except Exception as e:
        print(f"데이터 로드 중 오류: {e}")

# 실행 예시
# get_2day_food_plan("Busan", "YOUR_API_KEY")