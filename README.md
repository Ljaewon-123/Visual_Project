# 프로젝트 기능 간단설명

서울시의 반려동물시설현황 ,시각화및 분석

pip

- pip install requests
- pip install beautifulsoup4
- pip install selenium
- pip install django
- pip install matplotlib
- pip install seaborn
- pip install folium
- pip install base64



#### 나의 역할? 내가만든 기능?

1. 크롤링 
2. json 전처리 , 크롤링 데이터들을 원하는 형태로 재가공
2. Django
3. 카카오 API 활용 주소,좌표 변환기 
4. Geo_coding 
5. input값에 맞는 좌표를 folium 화면에 보여주고 마커를 한화면에 전부 찍어줌 
6. 우리동네 보고서 페이지(2_page.html)에 있는 Ajax, 해당 페이지에 활용된 views.py 부분 만듬 
7. 그외 만들거나 수정,추가된 많은 함수들이 views.py에 올라갔고 그것들을 Ajax활용해서 django 서버에 올림





사용 데이터 및 전체적은 코드 설명은 

**서울시 반려동물 시설 안내_**    PDF 참고



# Project_mypart

추후 최종본 업로드  == **real_real_final** 최종본

공용부분 프로젝트에서 내가 맡은 부분들 



같은 프로젝트 팀원 hongpower https://github.com/hongpower/project_visualization 

같이 commit 함 

아쉬운점 : 처음부터 git을 사용한게 아니라 팀원끼리의 코드 티키타카가 기록되지 못한게 아쉽다 
주/프로젝트 커밋의 뒤에 각팀원의 이름을 붙이기로함 
json total 에서 나온 결과 json 키값을 딕셔너리 안에 넣음 굉장히 천재적



일지



0214 

하루종일 주제선정



0215



 나는 카카오맵 에서 서울내로 크롤링 -> 당일완성
       카카오맵 띄우고 우측상단 이미지 눌러서 없애줬어함 
       검색을 진행하지만 왼쪽 정보창이 ajax로 가져오는거라 잘되지 않았음 
       그래서 시작하자마자 parser를 하는게 아니라 드라이버로 누를만한 버튼 다 눌러줘서 
       그다음 다시 parser해서 반복하는 방식 
       paginator 같은 경우는 더보기 누르면 2페이지로 가는데 다시 1페이지로 돌아와서 while true 와 for 문 if 로
       다음버튼이 눌리면 1~5페이지까지 자동 크롤링 하면서 중간에 광고는 빼주고 정보를 가져오게됨 
       그러다 다음버튼이 눌리지 않으면 while문을 종료함
       페이지가 6이든 12이든 지정된 id는 id1 ~ id5 로 같기에 for에서 처리하고 남는 부분은 try except로 예외처리하       였다



0216 



오전에는 카카오api로 주소를 좌표값으로 변환시켜주는 함수를 파이참에서 실행 성공함 
       오후에 크롤링 코드가 문제 목록이 많아서 더보기 버튼을 눌러야하면 상관이 없지만 
       목록이 1페이지를 넘어가지 않을때 에러발생 그당시 더보기 버튼을 xpath로 지정해놨는데 
       숨김 상태든 뭐든 xpath로 지정한 이상 계속 지정이 되어서 구분되지 못함 심지어 more라는 a태그의 클래스가 몇       개 더있었음 더보기 버튼을 id명으로 지정했는데 결과는 같음 이게 더보기 버튼이 생성이 안되는게 아니라
       클래스 이름이 바뀐상태로 hidden상태여서 그랬기 때문
       해서 검색 이후의 상태를 BeautifulSoup로 지정 클래스이름이 more HIDDEN인 a태그의 유무를 if 로 찾아서
       클릭과 클릭이 아닌것을 구분지음
       셀레니움과 BeautifulSoup은 서로 문법이 약간 다르다 띄어쓰기를 그대로 쓰냐 아니면 . 을 붙이냐 부터

​	같은 class 나 id를 구분지어줘야하냐 아니냐 다 알고있는거 같고 정확히 찍었는데도 안되는거 같으면

​       내가 문법을 바꿔서 한건지 아닌지를 신경써줘야 하고 정확한 사용법을 알고있어야 한다.
​	(드라이버는 for문이나 if문이 안되는건가??? )
​       5페이지에서 다음버튼이 활성화 되면 눌려주는방식인데 5페이지에서 딱 페이지가 끝나면 무한루프가 돌아버린다
​       xpath로 했는데 활성화 됬을때랑 안됬을때랑 xpath가 다름
​       더보기 버튼 문제와 똑같은 방법으로 해결함 셀레니움 객체는 for문이나 if에 true로 조건이 충족되지 않아서
​       결국 print(i)로 어디에서 부한 루프가 도는지 확인하고 문제의 다음버튼을 xpath로 지정해서 확인하는 if분을 

```python
 soup의 button = soup.find('button',class_='next disabled') 로 확인하고
    if button:
        break
    else:
        next_page = driver.find_element(By.XPATH, '/html/body/div[5]/div[2]/div[1]/div[7]/div[6]/div/button[2]')
        next_page.click()
```

​      와 같은 방법 으로 마무리 지었다
traceback (most recent call last):   셀레니움(드라이버)와 뷰티풀soup의 문법이 조금씩 달랐다 
어떤 에러가 났는지 추론가설로 맞췄어야했고 끝임없는 시도를했어야했다



0216 ~ 0217 

​	뽑아놓은 카카오,네이버 json파일을 각각 구별로 구분지어놓고 같은구에서 같은 이름을 가지고 있으면
​	네이버에서 뽑아온 주소를 배정하고 합친다. 
​	자세한 내용은 change_json 파일 참조



0217

​	구끼리 합치는 거에서 크게 몇가지 문제가 발생했는데 
​	하나는 띄어쓰기를 포함해서 같은 이름도 다르게 뽑는것이고 
​	다른 하나는 같은 이름을 지우면서 발생하는 문제였다 



```python
띄어쓰기 문제는 list_naver_name = list(map(lambda x: x['s_name'].replace(' ',''),naver_gu[gu_name]))
이런식으로 해결했고 
인덱스 에러는 for문을 역순으로 동작시켜서 해결했다
이후 구별로 정리된 json을 다시 한번 묶어주는 작업을 하면 끝난다.

이제 카카오톡 api 주소 -> 좌표 변환기를 사용 
그동안 통합한 json_total 을 사용해서 folium에 마커를 찍어주는 함수 생성함 
마커 이름은 각 가게의 's_name'로 만들고 파일경로 파일명,구 이름은 인풋받게함 

csv 파일같은 경우 사용 파일이 딱하나 이고 파일경로, 구 이름만 입력받게함 
좌표값이 이상해서 오픈api 함수사용 
pandas 사용해서 잘 정제하다가 for문에서 주소 -> 좌표 변환시 IndexError발생
혼자 형식이 이상하게 되어있는 데이터 발생 DataFrame 내에 데이터 수정 방법을 몰라 
일단 try except 로 IndexError를 걸러내고 출력함 
dataframe 문제가 있었는데 현재 주소를 가지고 동작하는 for문에서 folium marker에 들어갈 
병원이름을 따로 잡아주지 못한다는 문제였다 
여기서 i가 for문에서 돌고있는 주소가 서울 '구이름'이 하나씩 동작하고 
doro_add = hospital_data[hospital_data.도로명전체주소 == i]
        hosp_name = doro_add['사업장명'].values
        folium.Marker([local[0], local[1]], popup=folium.Popup(hosp_name[0], max_width=100)).add_to(center_loc)
해당 doro_add 라는 함수에 전체 csv에 도로명주소가 i와 [같은 행]을 찾아서
거기의 사업장명이라는 컬럼의 values만 가져와서 Popup(이름) 안에 넣어서 해결했다.
```

0218 



.. 뭔가 바빳고 기능적으로 많이 한듯 일단 모든 csv와 json이 좌표-> folium 과 마커표시가 가능하게 만듬
이걸 장고에 올리는 과정헤서 Open_Api 폴더를 장고 프로젝트 내부 폴더로 이동 (편하게 사용하기위함)
문제는 이 folium을 장고에 어떻게 올리느냐임
https://github.com/hongpower/project_visualization 같은 프로젝트 팀원 hongpower 의 프로젝트 장고 주소 

프로젝트 ajax관련 기능은 지수님이 코딩하셨고 그외 내가 만든 파일명과,구이름 만 들어가면 알아서 데이터에 주소를 좌표로 변환해서 화면은 구 시청으로 띄우고 필요한 마커를 표시해주는 프로그램을 
잘 섞어서 결론적으로 장고에서 ajax즉 동적으로 folium지도 데이터를 표시하는데 성공했다
화면공유를 통해 즉각적인 피드백을 해가고 서로 원할한 의사소통을 하면서 성공적인 결론에 도달했다.
도중에 팀원들과의 원할한 파일공유를 위해 파일위치와 경로를 통일함





0220 

장고 folium에서 csv파일도 가능하게 마커 이미지 외부 이미지로 바꾸기 
encoding 중에 euc-kr 과 cp949는 같다고 해도된다 cp949가 더 상위버전이기 때문

마커이미지를 다운받은 파일로 하면 for문에서 중첩으로 찍지 못하기 때문에 아래 두사이트에서 
마커이미지를 끌어와서 사용 

folium.Marker([37.5752205086784,127.012502773568],popup=folium.Popup('이쁜아이 공원면적:가능?',max_width=100),
              icon=folium.Icon(icon="plus",prefix='glyphicon',color='red')).add_to(my_loc)

중 icon 의 prefix 부분에 glyphicon 을 넣으면 http://bootstrapk.com/components/#glyphicons 여기서 아이콘을
prefix의 fa를 넣으면 fontawsome https://fontawesome.com/search?m=free 에서 아이콘을 가져온다.
꿀팁인듯 

어쩌다가 장고도 맡게됨

저번에 ajax로 동적 folium을 json파일 위치 뜨게 한거에 이어서 남은 csv파일도 뜨게 만들고 각각 상업명마다
마커 다르게 표시되게 하고 아래 나오는 리스트 목록도 파일마다 다르게 설정해주었다

카카오톡 API이용해서 내위치 띄워주는 코드를 가져옴 
내위치 띄워주는 자바스크립트 코드에서 이번엔 내가 직접 ajax를 사용 데이터를 GET으로 받고 처리해서
받은 좌표를 주소로 변환-> 해당 구만 가져옴





0221 



여기서 깃 제대로 쓰면서 병합 
.... 다른 사람 코드까지 받으니까 너무 햇갈린다 내 기준으로 새로운걸 위에다 쓰는게 맞나??
내 파일에다 끝까지 이어받아서 할려고 했는데 마지막에 만들어진거부터 합쳐지는 작업에 들어가니까 
너무 추가가 많아서 결국 clone 한거에서 장고 프젝 파일만 가져왔다. 이제부터 여기서 작업해야할듯
--> 가져온 프젝파일 가상환경 해줘서 바로바로 git push , pull 가능하게 만듬 



0222 



 csv가 , 가있으면 문제가 좀 있는듯 
fixed_function 여러 기능들을 만들거나 만질때 모든 요소를 확인해보지 못했다 
프로젝트 마감일이 다가오면서 기능들을 확인하고 있는데 몇몇 요소에서 에러가 발생했다
강동구에 애견카페 라던가 호텔 또는 약국의 결측치들 
예시를 강남구에서 했을때는 에러가 안났는데 갑자기 인덱스 에러가 발생 
일단 json파일의 에러는 카카오톡 api 가 반점(',') 을 잘 인식하지 못하는거 같다 주소를 크롤링으로 가져왔는데 
가게주인이 주소에 ','을 사용하면 좌표변환기가 인식을 못해서 에러가 발생하는 거라고판단 
replace(',','')으로 바꿔 주니 해결했다
이전에 csv파일을 folium으로 확인 마커까지 찍는 함수도 같은 에러가 발생해서
try 구문해결했던게 생각나서 csv함수도 해봤더니 거기는 replace가 있으나 마나 기능 차이가 없었다
아마 좀더 복합적인 문제로 에러가 발생하는것이고 csv파일은 공공데이터를 가져와서 데이터가 너무많아
어쩔수 없었다 내가 파일을 만든다면 전부 같은 형식으로 처리해야 이후 작업또한 편해진다는것을 깨달았다.
위 인덱스 에러와는 별개로 에러는 아니지만 약국같은 경우 도로명 주소가 없는 경우가 있었다 
매우 드문 경우라 마지막쯤 가서야 문제를 인지했고  ????? 해결했다 
--> csv 파일같은 경우 도로명 결측치를 fillna()로 소재지 전체 주소로 바꿔주는 작업이였다 
분석 도와줌 



0223 

폴더 같은 경로로 되어있는 파일 pull 받았는데 나혼자만 경로를 못찾았다 그럼 왜그러지?
주로 내가 만든거에서 예상치못한 에러나 버그 만 고쳤는데 
다른 팀원이 만든 코드를 내가 살짝이라도 응용 혹은 추가해서 다른기능이 되니까 생각보다는 재밌다고 느꼈다
남은시간 거이 scatter 그래프 애니매이션 할려고 했는데 실패했다 진척도가 없어서 시간이 너무 없었다.

원래 해당 깃허브 공간에 내가 만든 코드만 넣고 싶었는데 
팀원끼리의 코드가 얽히고 설키면서 그럴수가 없게되었다 장고 도입이후 부터는 (주소) 여기서 확인하는게 나을듯
깃허브 시작 후 초반에도 나는 push가 아니라 파일을 보내주거나 하는 식으로도 해서 내 모든 기록이 남지는 않은듯?

folium 같은거는 그려주는 함수가 3개가 필요해서 ajax로 따로 처리해주는 함수가 필요했지만
2_page같은 경우엔? 한가지 함수만 작동하면되서 매개변수에 얽매일 필요가없다

연습파일에서 만들고 장고에 적용하면서 소소하게 바뀌게됨 메인 기능은 변하지 않음



0224

머 여러가지함
2_page.html ajax부터 views.py 의 기능함수 까지 전부 내가 다 함
이제 부터 공유 깃허브에서 수정 함 

