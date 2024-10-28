![image](https://github.com/user-attachments/assets/f9303f69-4bf3-4d8e-9c10-55500e2bd28f)

## OOTB project
Outfit On The Body - 통계적 기법을 이용한 몸에 맞는 의류 추천 서비스

## 팀원 소개
- 김창선 - PM, Back-end
- 김창민 - 머신러닝, Back-end
- 방찬혁 - Back-end, 크롤링, DataBase
- 양준영 - Front-end, Back-end


## 프로젝트 소개
회원 가입시 입력한 정보로 신체 치수를 예측하여 의류 추천시 신체 치수와 일치하는 의류 사이즈를 추천하고, 후기를 통해 입력된 정보로 신체 치수를 보완하여 더 정확한 사이즈 추천이 가능합니다.

## 개발 기간
- 2024.07.02(화) ~ 2024.08.02(금)
- 계획 수립
- 요구사항 분석
- 설계 (DB, UI/UX, Web, 데이터 모델링)
- 기획 발표
- 구현
- 서비스 테스트
- 최종 발표

## 기대효과
- 의류 업체의 매출 증가 효과
- 사용자 불편 해소로 만족도 증가

## 개발환경
- Version : Java 1.6
- IDE : Eclipse
- Framework : Spring Framework 5.0.7
- ORM : Mybatis

## 기술 스택
- Server : Apache
- DataBase : MySQL
- WS/WAS : Tomcat
- 아이디어 회의 : Notion


## 프로젝트 아키텍쳐
### 시스템 아키텍처
![image](https://github.com/user-attachments/assets/8e6d7815-6c44-487d-bb8e-30d33adbe4f9)


### 메뉴 구성
![image](https://github.com/user-attachments/assets/f1f344bd-a055-4e72-b96d-b8d22c710a3a)


## 주요 기능
- 의류 추천 및 필터링
  
   비회원 - 키와 몸무게 입력시 신체치수를 예측하여 자동 입력

   회원 - 회원 가입시 저장된 정보로 자동 입력

- 위시리스트 기반 선호 의류 추천
- 위시리스트 추가, 삭제 및 필터링
- 후기 데이터로 정보 보완
- 사용자 문의사항 질문하기, 답변확인
- 회원 정보 수정
- 매니저 의류리스트 검색, 수정, 삭제 및 필터링
- 매니저 유저리스트 검색, 삭제 및 필터링
- 매니저 문의사항 질문확인, 답변하기
- 로그인, 회원가입, 회원탈퇴

![image](https://github.com/user-attachments/assets/66b76d7f-3c47-47bc-8dec-b1d4785fc8a1)
![image](https://github.com/user-attachments/assets/4e7fc105-9216-4023-b0f0-36b447e85b8e)
![image](https://github.com/user-attachments/assets/84770c20-7df4-4d29-8ea3-5114bba35e13)


### 트러블 슈팅
1. JSP 파일에서 자바스크립트의 리터럴(`)을 사용하여 변수 값을 삽입하려고 할 때, ${}구문이 JSP의 EL식으로 해석되어 오류 발생 원인으로 JSP 내장 표현식으로 처리하려 하기 때문에 발생함을 파악 해결방법으로 JSP에서 자바스크립트의 리터럴을 사용하는 경우 ${} 앞에 \(역슬래시)를 추가해 JSP가 이를 자바스크립트 구문으로 인식하도록 적용
![image](https://github.com/user-attachments/assets/275c0bbc-96e5-4c40-9007-75730e9992ec)



2. 모달을 여는 부분인 showModal 과 닫는 부분인 closeModal의 함수 중복 호출 문제 발생함을 파악

```
function showModal(productElement) {
    event.preventDefault();
    event.stopPropagation();
    console.log('showModal called');
    const modal = document.getElementById('myModal');
    const productName = productElement.querySelector('.product-name').textContent;
    const productPrice = productElement.querySelector('.discounted-price').textContent;
    const productImgSrc = productElement.querySelector('img').src;
    const productCategory = productElement.getAttribute('data-category');

    document.getElementById('modal-product-name').textContent = productName;
    document.getElementById('modal-product-price').textContent = productPrice;
    document.getElementById('modal-img').src = productImgSrc;

    // 모달 내용 동적 생성
    const tbody = modal.querySelector('tbody');
    tbody.innerHTML = generateModalContent(productCategory);

    modal.style.display = 'block';

    setTimeout(() => {
        modal.addEventListener('click', function(e) {
            if (e.target === modal) {
                closeModal();
            }
        });
    }, 100);
}

```
```
function closeModal() {
    event.stopPropagation(); // 이벤트 전파 중지
    document.getElementById('myModal').style.display = 'none';
}
```
중복된 showModal과 closeModal 함수 정의를 하나로 통합해 이벤트 리스너를 중복으로 추가하지 않도록 하여 문제 해결
```
function showModal(productElement) {
    event.preventDefault();
    event.stopPropagation();
    console.log('showModal called');
    const modal = document.getElementById('myModal');
    const productName = productElement.querySelector('.product-name').textContent;
    const productPrice = productElement.querySelector('.discounted-price').textContent;
    const productImgSrc = productElement.querySelector('img').src;
    const productCategory = productElement.getAttribute('data-category');

    document.getElementById('modal-product-name').textContent = productName;
    document.getElementById('modal-product-price').textContent = productPrice;
    document.getElementById('modal-img').src = productImgSrc;

    // 모달 내용 동적 생성
    const tbody = modal.querySelector('tbody');
    tbody.innerHTML = generateModalContent(productCategory);

    modal.style.display = 'block';

    // 이벤트 리스너를 한번만 추가하도록 수정
    modal.onclick = function(e) {
        if (e.target === modal) {
            closeModal();
        }
    };
}

function closeModal() {
    document.getElementById('myModal').style.display = 'none';
}

```


## Main Tools
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=Python&logoColor=white"><img src="https://img.shields.io/badge/java-007396?style=for-the-badge&logo=OpenJDK&logoColor=white"><img src="https://img.shields.io/badge/Spring-6DB33F?style=for-the-badge&logo=Spring&logoColor=white"><img src="https://img.shields.io/badge/Spring Security-6DB33F?style=for-the-badge&logo=Spring Security&logoColor=white"><img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=MySQL&logoColor=white"><img src="https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=Flask&logoColor=white"><img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=HTML5&logoColor=white"><img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=CSS3&logoColor=white"><img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=JavaScript&logoColor=white">



### 피드백 내용
- 주제 선정의 아이디어는 우수함
- 그러나 구현시 입력 파라미터인 키와 몸무게는 너무 적어 의류 신체 사이즈를 추천하기에는 부족하다고 판단됨
- 머신러닝을 위한 학습 데이터 확보가 중요함
- 각각의 회사별로 브랜드 특성에 따라 같은 사이즈이지만 다른 치수를 설정해서 만드는 회사들의 표준을 어떻게 맞출 수 있을지 구체화하면 좋을것 같음
- 이 아이템이 플랫폼을 만들어 상품을 등록할 때 해당 치수를 넣는 식인지, API형태로 타 플랫폼에 제공하는 것인지, BM에 대한 확장을 하면 좋을 것 같음
- 개인의 치수를 예측해서 알려주더라도 정확도가 떨어질 수 있는데, 사용자가 제품을 보고 사용자 후기를 어떤식으로 DB에 비교하고 
후기의 신뢰도를 어떻게 평가하고 적용할 것인지 구체화 하면 좋을 것 같음
- 옷을 추천하려면 각각의 브랜드 상품을 등록할 때 명확한 치수를 넣어줘야 하는데, 수많은 상품의 치수를 표준화해서 넣는 방법에 대한 기술 필요

- 조언 : 키 몸무게 성별정도 + 사진을 더해서 치수를 제공한다면 좋을 것 같음
- 초기 입력 데이터의 편의성
- 전체적인 프로젝트의 프로세스 파악
