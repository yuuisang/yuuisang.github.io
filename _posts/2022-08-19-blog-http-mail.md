---
layout: post
title: "[Blog] HTML form태그에서 메일보내기 : Google Apps Mail"
date: 2022-08-19 10:00:00 +0600
categories: [Blog]
author: EuiSangYu
post_image: "/assets/images/blog/html_mail.png"
---

티스토리에서 깃허브 블로그로 넘어오면서 내 블로그를 방문한 사람들이 전달하고 싶은 말을 바로 나에게 편하게 보낼 수 있도록 메일 서비스를 적용하고 싶었다.

HTML에서 `mailto`를 사용하면, 구현은 간단하지만 outlook 등 같은 서드파티 앱을 실행해 직접 메일을 보내는 방식이기 때문에 내가 생각한 편리함은 없었다.

하지만 역시 세상은 넓고 똑똑한 사람은 많다보니 이런 기능을 적용해본 블로거분이 계셔서 그 분의 글을 보며 `별도 서버가 없는 순수 HTML과 자바스크립트`로 메일보내기를 구현할 수 있었다.

내가 바라던대로 방문자(사용자)는 계정에 로그인하고 메일을 보내는 귀찮음을 느낄 필요도 없이 간단한 웹페이지의 양식대로만 입력해서 쉽고 빠르게 메일을 보낼 수 있다.

이 방법을 찾기 전에는 서버를 하나 결제해야하나 고민했는데 구글에서 제공하는 방법으로 우회해서 해결할 수 있어서 다행이었다😢

<br>

[참고한 사이트](https://kutar37.tistory.com/entry/%EC%A0%95%EC%A0%81-HTML-form%ED%83%9C%EA%B7%B8%EC%97%90%EC%84%9C-%EB%A9%94%EC%9D%BC%EB%B3%B4%EB%82%B4%EA%B8%B0-Google-Apps-Mail)

<br>

## 메일 보내는 페이지(화면)

![image](https://user-images.githubusercontent.com/58925978/187122577-510b97eb-c777-41e9-877d-aa5c07b4d9de.png)

위 사진은 내 블로그에서 전달할 내용과 정보를 입력하는 페이지이다.
페이지는 이미 구성을 했고, 이제 기능을 구현해보자.

우선 참고한 사이트에서 진행한 방식 그대로 따라가봤다.

## Google Apps Mail을 사용해 정적 HTML Form에서 메일을 보내기

작동 예제
[링크](https://dwyl.github.io/learn-to-send-email-via-google-script-html-no-server/)

### 동작 원리
유지보수가 필요한 서버를 이용해 이메일을 보내는 대신, <u>사용자를 대신하여 Google로 메일을 보내고 Google 스프레드시트를 사용해 데이터를 추적</u>하는 방식

### 진행 시작
#### 1. Sample Spreadsheet를 복사
[https://docs.google.com/spreadsheets/d/1Bn4m6iA_Xch1zzhNvo_6CoQWqOAgwwkOWJKC-phHx2Q/copy](https://docs.google.com/spreadsheets/d/1Bn4m6iA_Xch1zzhNvo_6CoQWqOAgwwkOWJKC-phHx2Q/copy)

본인 Google 계정에 로그인하고 "사본 만들기"를 클릭

![image](https://user-images.githubusercontent.com/58925978/187122597-e65ea2fe-1c9e-49be-b090-93eb23a45ec5.png)

사본 만들기를 클릭하고 나면 이렇게 클라우드에서 사본이 열린다.

#### 2. 스크립트 편집기 열기
메뉴에서 `확장프로그램` -> `Apps Script` 를 클릭한다.

> 위에 가이드 문서에서는 `도구` -> `스크립트편집기` 라고 나와있는데 나는 메뉴가 달라 저렇게 구성되어 있었다.. 아마 버전의차이아닐까

#### 3. 스크립트에서 TO_ADDRESS 를 설정
![image](https://user-images.githubusercontent.com/58925978/187122620-5d12c4aa-6e17-4e6b-9134-a961be3df119.png)

해당 빨간 밑줄 부분을 `본인 메일주소`로 수정

#### 4. 스크립트의 새로운 버전 저장
![image](https://user-images.githubusercontent.com/58925978/187122648-b8f55a3c-ab18-4bd7-888b-fec84a1ef029.png)

메뉴에서 `파일` -> `버전기록` -> `현재버전 이름저장` 클릭
![image](https://user-images.githubusercontent.com/58925978/187122675-2f0280b6-dc39-4d1d-ae8e-a5d33b1a6140.png)

여기까지 완료했다면

#### 5. 업데이트된 스크립트를 웹 앱으로 배포

![image](https://user-images.githubusercontent.com/58925978/187122697-3f713693-597a-4e40-9a89-a84c6239be0c.png)

해당 스크립트 안에서 `배포` -> `새 배포` 클릭

![image](https://user-images.githubusercontent.com/58925978/187122711-7cfcaa2e-0c8b-4930-89d4-bf930e4b7ebd.png)

아무 설명이나 써넣고 `배포` 클릭

#### 6. 이메일을 보내기 위해 스크립트를 인증

![image](https://user-images.githubusercontent.com/58925978/187122743-61ca440e-45ca-45b1-a3f6-c8f21fbe044a.png)

해당 인증 부분 캡처들을 못 찍어서 `참조 이미지로 대체`함.

![image](https://user-images.githubusercontent.com/58925978/187122772-a4f6a848-43da-4830-9242-9ab39c55dc79.png)

이제 배포 ID와 웹 URL을 메모장 같은 곳에 기록해두고 마무리!
> 잊어버려도 `배포관리` 메뉴에 들어가면 다시 확인할 수 있음.

![image](https://user-images.githubusercontent.com/58925978/187122793-a626be3e-606d-497e-af28-b991d08be925.png)

#### 7. 이제 실제 화면 페이지를 구성(HTML)

이건 사람마다 본인이 원하는 화면 구성이 다 다를테니 내 블로그 코드를 예로 보여주자면

```html
---
layout: page
title: 연락하기
---
<div class="contact-area bg-color1 p-t-130 p-b-130">
   <div class="container">
      <article class=""  data-aos="fade-up">
         <div class="row m-b-60">
            <div class="col-md-4">
               <div class="contact-info">
                  <div class="info-logo"><img src="{{site.baseurl}}/assets/images/contact-info-logo.png" alt="contact info logo"/></div>
                  <div class="info-content">
                     <h5 class="heading-5"><a href="#">Office Address</a></h5>
                  </div>
               </div>
            </div>
            <div class="col-md-4">
               <div class="contact-info">
                  <div class="info-logo"><img src="{{site.baseurl}}/assets/images/contact-info-logo2.png" alt="contact info logo"/></div>
                  <div class="info-content">
                     <h5 class="heading-5"><a href="#">Email Address</a></h5>
                  </div>
               </div>
            </div>
            <div class="col-md-4">
               <div class="contact-info m-0">
                  <div class="info-logo"><img src="{{site.baseurl}}/assets/images/contact-info-logo3.png" alt="contact info logo"/></div>
                  <div class="info-content">
                     <h5 class="heading-5"><a href="#">Phone Number</a></h5>
                  </div>
               </div>
            </div>
         </div>
         <div class="row">
            <div class="col-md-7">
               <div class="comment-form">
                  <!-- <script data-cfasync="false" type="text/javascript" src="https://cdn.rawgit.com/dwyl/html-form-send-email-via-google-script-without-server/master/form-submission-handler.js"></script> -->
                  <div class="inner-title">
                     <h5 class="heading-5">Send Your Message</h5>
                  </div>
                  <form id="emailForm" class="gform" method="POST" data-email="clothes.yoo@gmail.com" 
                        action="https://script.google.com/macros/s/AKfycbzm-PBHodHx2va9AAauDKxBxYOybY37cHxzQVRy6Qq6hJ5kqpSObQVUi-FcdJ612QUR/exec">
                     <div class="form-row">
                        <div class="col-md-12">
                           <div class="form-row">
                              <div class="col-md-12">
                                 <div class="form-group">
                                    <input type="text" class="form-control" id="senderEmail" name="senderEmail" placeholder="Your Email" required>
                                 </div>
                              </div>
                           </div>
                           <div class="form-row">
                              <div class="col-md-12">
                                 <div class="form-group">
                                    <input type="text" class="form-control" id="senderName" name="senderName"placeholder="Your Name" required>
                                 </div>
                              </div>
                           </div>
                           <div class="form-row">
                              <div class="col-md-12">
                                 <div class="form-group">
                                    <textarea class="form-control" id="message" name="message" rows="5" placeholder="Your Message"></textarea>
                                 </div>
                              </div>
                           </div>
                           <script type="text/javascript">
                              (function() {
                                 // get all data in form and return object
                                 function getFormData(form) {
                                    var elements = form.elements;
                                    var honeypot;

                                    var fields = Object.keys(elements).filter(function(k) {
                                       if (elements[k].name === "honeypot") {
                                       honeypot = elements[k].value;
                                       return false;
                                       }
                                       return true;
                                    }).map(function(k) {
                                       if(elements[k].name !== undefined) {
                                       return elements[k].name;
                                       // special case for Edge's html collection
                                       }else if(elements[k].length > 0){
                                       return elements[k].item(0).name;
                                       }
                                    }).filter(function(item, pos, self) {
                                       return self.indexOf(item) == pos && item;
                                    });

                                    var formData = {};
                                    fields.forEach(function(name){
                                       var element = elements[name];
                                       
                                       // singular form elements just have one value
                                       formData[name] = element.value;

                                       // when our element has multiple items, get their values
                                       if (element.length) {
                                       var data = [];
                                       for (var i = 0; i < element.length; i++) {
                                          var item = element.item(i);
                                          if (item.checked || item.selected) {
                                             data.push(item.value);
                                          }
                                       }
                                       formData[name] = data.join(', ');
                                       }
                                    });

                                    // add form-specific values into the data
                                    formData.formDataNameOrder = JSON.stringify(fields);
                                    formData.formGoogleSheetName = form.dataset.sheet || "responses"; // default sheet name
                                    formData.formGoogleSendEmail
                                       = form.dataset.email || ""; // no email by default

                                    return {data: formData, honeypot: honeypot};
                                 }

                                 function handleFormSubmit(event) {  // handles form submit without any jquery
                                    event.preventDefault();           // we are submitting via xhr below
                                    var form = event.target;
                                    var formData = getFormData(form);
                                    var data = formData.data;

                                    // If a honeypot field is filled, assume it was done so by a spam bot.
                                    if (formData.honeypot) {
                                       return false;
                                    }

                                    disableAllButtons(form);
                                    var url = form.action;
                                    var xhr = new XMLHttpRequest();
                                    xhr.open('POST', url);
                                    // xhr.withCredentials = true;
                                    xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
                                    xhr.onreadystatechange = function() {
                                       if (xhr.readyState === 4 && xhr.status === 200) {
                                          form.reset();
                                          var formElements = form.querySelector(".form-elements")
                                          if (formElements) {
                                             formElements.style.display = "none"; // hide form
                                          }
                                          var thankYouMessage = form.querySelector(".thankyou_message");
                                          if (thankYouMessage) {
                                             thankYouMessage.style.display = "block";
                                             alert("메일 전송에 성공했습니다. 확인 후 회신드리겠습니다.");
                                          }
                                       }
                                    };
                                    // url encode form data for sending as post data
                                    var encoded = Object.keys(data).map(function(k) {
                                       return encodeURIComponent(k) + "=" + encodeURIComponent(data[k]);
                                    }).join('&');
                                    xhr.send(encoded);
                                 }
                                 
                                 function loaded() {
                                    // bind to the submit event of our form
                                    var forms = document.querySelectorAll("form.gform");
                                    for (var i = 0; i < forms.length; i++) {
                                       forms[i].addEventListener("submit", handleFormSubmit, false);
                                    }
                                 };
                                 document.addEventListener("DOMContentLoaded", loaded, false);

                                 function disableAllButtons(form) {
                                    var buttons = form.querySelectorAll("button");
                                    for (var i = 0; i < buttons.length; i++) {
                                       buttons[i].disabled = true;
                                    }
                                 }
                                 })();
                           </script>
                           <div class="form-group m-0">
                              <button id="btnSubmit" class="btn-submit mt-2">Send Message</button>
                           </div>
                        </div>
                     </div>

                     <div style="display:none" class="thankyou_message">
                        <h2><em>Thanks</em> for contacting us! We will get back to you soon!</h2>
                     </div>
                  </form>
               </div>
            </div>
            <div class="col-md-4 offset-md-1">
               <div class="contact-image"><img src="{{site.baseurl}}/assets/images/contact-image.png" alt="contact image"/></div>
            </div>
         </div>
      </article>
   </div>
</div>

```
<br>

이렇게 구성되어 있다.

#### 8. 주의사항

```html
1. 만약 이 레포지토리의 예제가 아닌 직접 작성한 form을 벌써 사용하려고 한다면 각각의 form 요소 name 속성은 Google 시트의 컬럼네임과 같아야 한다.

2. form태그의 class는 gform이 되어야 함. 즉, <form class = "gform">

3. Form태그의 action 속성을 전 단계에서 복사해놓은 URL로 고쳐야 함을 잊지 말 것!!(중요)

```
![image](https://user-images.githubusercontent.com/58925978/187122825-dc72e3b8-a115-4223-ae50-738be3818aba.png)

#### 9. 브라우저에서 HTML Form (페이지) 열기

1. HTML Form에서 테스트 데이터를 채움

![image](https://user-images.githubusercontent.com/58925978/187122852-c9fc81d2-3d3c-42db-bfdd-974e82cbf5f1.png)

2. submit 버튼 클릭 후 json 결과 데이터 확인
![image](https://user-images.githubusercontent.com/58925978/187122867-3f18e881-341f-45fd-a7eb-3a90a3f95699.png)

참고로 위 2개의 캡처는 참조용 이미지임.

#### 10. 아까 설정했던 본인 메일주소로 들어가 받은편지함을 확인

![image](https://user-images.githubusercontent.com/58925978/187122897-efcff9bc-176b-43a2-9c75-386cfa699382.png)

#### 11. JavaScript 와 "AJAX" 를 사용한 양식 제출 + 양식이 제출될 때 나오는 메시지 커스터마이징

여기서부턴 꼭 필요한 과정은 아니지만 사용자 편리성을 위해 필요하다고 볼 수있는 부분이다.

```
페이지가 JSON 응답/결과로 변경되지 않도록 하려면 `AJAX`를 사용하여 양식을 제출해야 한다.

파일 끝 (*</body> 태그 닫기 전)에 다음 JavaScript 파일을 포함하도록 index.html을 업데이트.

<script data-cfasync="false" type="text/javascript"
src="https://cdn.rawgit.com/dwyl/html-form-send-email-via-google-script-without-server/master/form-submission-handler.js"></script>

```

참고로 
> 위의 3단계에서 TO_ADDRESS 변수를 설정하지 않은 경우, 메인 form 요소에 data-email="example@email.net"를 포함시켜야 된다.

#### 12. thankyou_message div를 만들어 직접 메시지를 만든다

```html
<!-- 해당 div의 위치는 <form> 태그의 안에 속하게 할 것. -->

<div style="display:none" class="thankyou_message">
 <!-- You can customize the thankyou message by editing the code below -->
 <h2><em>Thanks</em> for contacting us! We will get back to you soon!
 </h2>
</div>
```

![image](https://user-images.githubusercontent.com/58925978/187122929-4530c0f4-93c0-4768-9fc8-302f61ce60bd.png)

사용자들에게 전송이 잘 되었다는것을 알리기 위한 것이므로 나는 Alert 메세지까지 추가했다.

![image](https://user-images.githubusercontent.com/58925978/187122976-6a369e42-e340-4727-b134-4df94f01f2ac.png)

---

# 마무리

여기까지만 하면 일단 기능적으로는 전부 끝났다.
CSS 나 메일 수신시 양식을 변경하는 것은 반드시 해야하는 기능은 아니기 때문에 작성하지 않으려고 한다.

시도하는 모든 사람들 화이팅🔥





