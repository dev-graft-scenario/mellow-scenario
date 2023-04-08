# Mellow

온라인 의류 쇼핑몰 개발 의뢰가 들어왔습니다!

우리가 만들 서비스의 이름은 **[Mellow]** 다양한 카테고리로 구분된 의류를 판매하려 합니다!

## 시나리오
**사용자 인증**
- 회원가입: 사용자는 회원가입 절차를 거쳐 쇼핑몰에 가입할 수 있습니다.
- 로그인: 가입한 사용자는 아이디와 패스워드를 사용해 로그인을 할 수 있습니다.

**의류 상품 관리**
- 의류 상품 검색: 사용자는 검색어를 입력하여 관심있는 의류 상품을 검색할 수 있습니다.
- 카테고리별 의류 상품 목록 조회: 사용자는 카테고리별로 의류 상품 목록을 조회할 수 있습니다.
- 의류 상품 상세 정보 조회: 사용자는 의류 상품의 상세 정보를 조회할 수 있습니다.

**장바구니**
- 의류 상품 담기: 사용자는 의류 상품을 장바구니에 담을 수 있습니다.
- 장바구니 목록 조회: 사용자는 장바구니에 담긴 의류 상품 목록을 조회하고, 수량 변경 및 상품을 삭제할 수 있습니다.

**주문 및 결제**
- 주문 정보 입력: 사용자는 배송지 정보, 결제 방법, 배송 요청 사항 등을 입력합니다.
- 결제 진행: 사용자는 선택한 결제 수단을 통해 결제를 진행합니다.
- 주문 내역 조회: 사용자는 주문 내역을 조회하고, 출고 상태를 확인할 수 있습니다.

**의류 상품 후기 및 평점**
- 의류 상품 후기 작성: 구매한 의류 상품에 대해 후기를 작성하고, 평점을 남길 수 있습니다.
- 후기 목록 조회: 사용자는 의류 상품에 대한 다른 사용자들의 후기와 평점을 조회할 수 있습니다.


## Project Spec

**프로젝트 구성**
| Name | Version |
|:---|:---|
|Spring Boot | 2.7.3 |
|Kotlin | |
|Gradle | 7.5 |

**개발환경**
|Name | Desc|
|:---|:---|
|Architecture | Hexnagonal |
|DB| H2 |

**기본 의존성**
| Name | Desc |
|:---|:---|
|H2| |

**프로젝트 패키지 구조**
| Name | Desc |
|:---|:---|
| | |

## Schemas

### 사용자 정보(user/users)

| Column Name  | Data Type | Description               |
|:-------------|:----------|:--------------------------|
| id           | Long      | 사용자의 고유 식별자 (Primary Key) |
| email        | String    | 사용자의 이메일 주소 (Unique)      |
| password     | String    | 사용자의 비밀번호 (암호화된 형태로 저장)   |
| name         | String    | 사용자의 이름                   |
| phone_number | String    | 사용자의 전화번호                 |
| created_at   | DateTime  | 계정 생성 날짜                  |
| updated_at   | DateTime  | 계정 정보 수정 날짜               |


### 상품 정보(product/products)

| Column Name | Data Type | Description                                 |
|:------------|:----------|:--------------------------------------------|
| name        | String    | 상품 이름                                       |
| category_id | Long      | 상품 카테고리 ID (Foreign Key, 참조: categories.id) |
| price       | Decimal   | 상품 가격                                       |
| description | Text      | 상품 설명                                       |
| image_url   | String    | 상품 이미지 URL                                  |
| created_at  | DateTime  | 상품 등록 날짜                                    |
| updated_at  | DateTime  | 상품 정보 수정 날짜                                 |

### 상품 카테고리(category/categories)

| Column Name | Data Type | Description                |
|:------------|:----------|:---------------------------|
| id          | Long      | 카테고리의 고유 식별자 (Primary Key) |
| name        | String    | 카테고리 이름                    |

### 주문 정보(order/orders)

| Column Name  | Data Type | Description                             |
|:-------------|:----------|:----------------------------------------|
| id           | Long      | 주문의 고유 식별자 (Primary Key)                |
| user_id      | Long      | 주문한 사용자의 ID (Foreign Key, 참조: users.id) |
| order_status | String    | 주문 상태 (예: 결제 완료, 배송 중, 배송 완료)           |
| total_price  | Decimal   | 주문의 총 가격                                |
| created_at   | DateTime  | 주문 생성 날짜                                |
| updated_at   | DateTime  | 주문 정보 수정 날짜                             |

### 주문 상품 정보(order_item/order_items)

| Column Name | Data Type | Description                           |
|:------------|:----------|:--------------------------------------|
| id          | Long      | 주문 상품의 고유 식별자 (Primary Key)           |
| order_id    | Long      | 주문 정보 ID (Foreign Key, 참조: orders.id) |
| product_id  | Long      | 상품 ID (Foreign Key, 참조: products.id)  |
| quantity    | Integer   | 주문 상품의 수량                             |
| price       | Decimal   | 주문 상품의 가격                             |

###상품 후기 (review/reviews)

| Column Name | Data Type | Description                                 |
|:------------|:----------|:--------------------------------------------|
| id          | Long      | 후기의 고유 식별자 (Primary Key)                    |
| user_id     | Long      | 후기 작성자의 사용자 ID (Foreign Key, 참조: users.id)  |
| product_id  | Long      | 후기 대상 상품의 ID (Foreign Key, 참조: products.id) |
| rating      | Integer   | 사용자가 부여한 상품 평점 (1-5)                        |
| content     | Text      | 후기 내용                                       |
| created_at  | DateTime  | 후기 작성 날짜                                    |

### 장바구니 상품 정보 (cart_item/cart_items)
| Column Name | Data Type | Description                                 |
|:------------|:----------|:--------------------------------------------|
| id          | Long      | 장바구니 상품의 고유 식별자 (Primary Key)               |
| user_id     | Long      | 장바구니 주인의 사용자 ID (Foreign Key, 참조: users.id) |
| product_id  | Long      | 상품 ID (Foreign Key, 참조: products.id)        |
| quantity    | Integer   | 장바구니 상품의 수량                                 |

## Goals
- ✅ 멀티 모듈 구조 학습
- ✅ Hexagonal 구조 학습
- ✅ 마이크로서비스 단위 개발 학습

## 아래는 fork 이후 직접 작성해주세요.

### :pushpin: 참여 팀원
|     [팀원 닉네임](팀원-프로필-주소)      |
|:----------------------------:|
|  <img src="" width="100px">  |
| BE, FE, IOS, ANDROID, DESIGN |
|            한줄 설명             |

--- 
### :screwdriver: 기술 스택
<p align="center">
<img src="https://img.shields.io/badge/TypeScript-569A31?style=for-the-badge&logo=JavaScript&logoColor=white" alt="">
<img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=TypeScript&logoColor=white" alt="">
<img src="https://img.shields.io/badge/JAVA-007396?style=for-the-badge&logo=java&logoColor=white" alt="">
<img src="https://img.shields.io/badge/Kotlin-2496ED?style=for-the-badge&logo=kotlin&logoColor=orange" alt="">
<img src="https://img.shields.io/badge/ReactNative-2496ED?style=for-the-badge&logo=react&logoColor=white" alt="">
</p>
<p align="center">
<img src="https://img.shields.io/badge/IOS-white?style=for-the-badge&logo=apple&logoColor=black" alt="">
<img src="https://img.shields.io/badge/Android-green?style=for-the-badge&logo=android&logoColor=white" alt="">
<img src="https://img.shields.io/badge/react-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="">
<img src="https://img.shields.io/badge/Testing Library-E33332?style=for-the-badge&logo=testingLibrary&logoColor=white" alt="">
<img src="https://img.shields.io/badge/React Router-CA4245?style=for-the-badge&logo=reactRouter&logoColor=white" alt="">
</p>
<p align="center">
<img src="https://img.shields.io/badge/Spring Boot-6DB33F?style=for-the-badge&logo=Spring Boot&logoColor=white" alt="" >
<img src="https://img.shields.io/badge/JUnit5-25A162?style=for-the-badge&logo=JUnit5&logoColor=white" alt="">
<img src="https://img.shields.io/badge/mariaDB-003545?style=for-the-badge&logo=mariaDB&logoColor=white" alt="">
<img src="https://img.shields.io/badge/Hibernate-59666C?style=for-the-badge&logo=Hibernate&logoColor=white" alt="">
<img src="https://img.shields.io/badge/Amazon AWS-232F3E?style=for-the-badge&logo=Amazon AWS&logoColor=white" alt="">
</p>
<p align="center">
<img src="https://img.shields.io/badge/Amazon S3-569A31?style=for-the-badge&logo=Amazon S3&logoColor=white" alt="">
<img src="https://img.shields.io/badge/NGINX-009639?style=for-the-badge&logo=NGINX&logoColor=white" alt="">
<img src="https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=Jenkins&logoColor=white" alt="">
<img src="https://img.shields.io/badge/SonarQube-4E9BCD?style=for-the-badge&logo=SonarQube&logoColor=white" alt="">
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=white" alt="">
</p>

### 
