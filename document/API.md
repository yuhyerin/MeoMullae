# API

## SIGNUP

POST

http://127.0.0.1:8000/api/account/signup/

- BODY
  - username
  - email
  - password1
  - password2



## USER_DETAIL

POST

http://127.0.0.1:8000/api/accounts/user_detail/

- HEADERS
  - {"Authorization" :  "Token abcde12345"}
- BODY
  - username
  - email
  - usertype
    - 사업자일 경우
      - 0
    - 일반 사용자일 경우
      - 1
  - gender
    - 남성
      - 0
    - 여성
      - 1
  - address
  - birth_year
    - 길이 4 최대 설정
      - ex> 2002
  - (아래는 사업자일 경우만 - 이미지는 추가할 예정)
  - biznumber
  - bizname
  - bizaddress
  - bizimage



## LOGIN

POST

http://127.0.0.1:8000/api/account/login/

- BODY
  - email
  - password



## LOGOUT

POST

http://127.0.0.1:8000/api/account/logout/

- HEADERS
  - {"Authorization" :  "Token abcde12345"}




## PASSWORD CHANGE

POST

http://127.0.0.1:8000/api/account/password/change/

- BODY
  - new_password1
  - new_password2
  - old_password
- HEADERS
  - {"Authorization" :  "Token abcde12345"}

- error.response.data의 예시

```
{
    "new_password2": [
        "비밀번호가 너무 짧습니다. 최소 8 문자를 포함해야 합니다.",
        "비밀번호가 너무 일상적인 단어입니다.",
        "비밀번호가 전부 숫자로 되어 있습니다."
    ]
}
```





## STORES

POST

http://127.0.0.1:8000/api/stores/store_category/

- 카테고리에 해당하는 모든 식당 리스트
- BODY
  - category
- HEADERS
  - {'Authorization': 'Token a1sd3fa5sdf531'}



POST

http://127.0.0.1:8000/api/stores/store_list/

- 카테고리와 유저의 주소지와 맞는 모든 식당 리스트

- Body
  - category
  - user_location
- Headers
  - {'Authorization': 'Token a1sd3fa5sdf531'}



POST

http://127.0.0.1:8000/stores/store_detail/ (X)

http://127.0.0.1:8000/api/stores/<<int:store_pk>>/ (O)

- 식당의 고유 id 정보를 URL 담아서 보내주면 식당 정보 리턴
- 주의할점은 DB에 넣으면서 순서대로 생기는 pk값이 아니라 처음에 데이터 자체가 갖던 식당 id 값이다.
- Headers
  - {'Authorization': 'Token a1sd3fa5sdf531'}



## REVIEWS

POST, DELETE

http://127.0.0.1:8000/api/reviews/12345/

- URL에 리뷰 데이터의 pk 값을 담아서 보내야 한다
- 서버에서는 보내준 pk 값에 해당하는 리뷰 정보를 리턴
- Headers
  - {'Authorization': 'Token a1sd3fa5sdf531'}



POST

http://127.0.0.1:8000/api/reviews/store_review_list/

- 특정 식당의 리뷰 데이터 전체
- BODY
  - storeid
- HEADERS
  - {'Authorization': 'Token a1sd3fa5sdf531'}



POST

여기 모델링 수정 필요(Review 모델에 User:Review = 1:N 관계 필요)

user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.SET_NULL, null=True) 이렇게 해서 굳이 유저 모델도 지워지는 일 없도록 하는게 좋을 듯

http://127.0.0.1:8000/api/reviews/create_review/

- 식당의 리뷰 작성
- 주의할 점은 BODY에 담을 store_id는 store가 애초에 갖던 고유 id값이 아니라 db에 저장되는 순서를 담은 pk값이다.
- BODY
  - store_id
  - title
  - content
- HEADERS
  - {"Authorization": "Token asdflaj123489235"}



## Order

POST

http://127.0.0.1:8000/api/accounts/user_order/

- 유저의 주문 주소 추가

- BODY
  - location
- HEADERS
  - {"Authorization": "Token asdflaj123489235"}



POST

http://127.0.0.1:8000/api/accounts/user_order_list/

- 유저의 주문 리스트(최신순 5개)
- HEADERS
  - {"Authorization": "Token asdflaj123489235"}



## Advertisement

POST

http://127.0.0.1:8000/api/advertisements/register_ad/

- 광고 등록
- BODY
  - id_store
  - image
- Headers
  - {"Authorization": "Token asdflaj123489235"}



POST

http://127.0.0.1:8000/api/advertisements/find_store/

- 광고 등록할때 가게 이름 검색시
- BODY
  - store_name
- Headers
  - {"Authorization": "Token asdflaj123489235"}



POST

http://127.0.0.1:8000/api/advertisements/register_ad_info/

- 특정 광고에 대한 디테일 정보
- BODY
  - id_store
- Headers
  - {"Authorization": "Token asdflaj123489235"}



POST

http://127.0.0.1:8000/api/advertisements/bizuser_ad_info/

- 광고주가 자신이 광고하는 가게들의 모든 목록 조회시
- Headers
  - {"Authorization": "Token asdflaj123489235"}



POST

http://127.0.0.1:8000/api/advertisements/ad_to_main/

- 일반 유저가 로그인시 메인 페이지에 띄울 광고
- BODY
  - email
- Headers
  - {"Authorization": "Token asdflaj123489235"}



POST

http://127.0.0.1:8000/api/advertisements/click_ad/

- 광고 이미지 클릭했을 경우(몇번 클릭됐는지 정보 얻기 위함)
- BODY
  - id_store
  - advertisement_id
- Headers
  - {"Authorization": "Token asdflaj123489235"}



POST

http://127.0.0.1:8000/api/advertisements/bizuser_ad_click_info/

- 광고주에게 광고별 클릭 수 정보 제공
- Headers
  - {"Authorization": "Token asdflaj123489235"}





