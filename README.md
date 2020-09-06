# zoom-clone-study

## 2020-09.06 시작.
2020 – 9,6

zoom clone study – web dev simplified 의 how to create a video chat app with WebRTC 라는 영상을 통해 공부한 것을 정리한다. 

웹어플리케이션을 만들기 위해 node.js 의 프레임 워크인 express를 이용한다. 
require(‘express’)를 이용하여 express를 로드하고, 변수에 담아 제어한다. 
이 두줄을 이용한다. 이것은 프레임워크의 제작자가 만든 이용법이다.
const  express  = require ('express')
const  app  = express ()

다음으로 통신을 위한 http 서버를 생성한다. listen을 이용하여 3000포트를 할당하였다.
const  server  = require ('http').Server (app )
server .listen (3000 )


다음으로는 웹 소켓을 이용해 양방향 통신을 구현하도록 한다. 이때 필요한 것은 node.js의 프레임 워크인 socket.io 이다.
const  io  = require ('socket.io')(server )

이때 socket.io에서 중요한 함수가 있는데,
emit - 서버는 클라이언트에게로, 클라이언트는 서버에게로 데이터를 보낸다
on - 서버는 클라이언트에게로, 클라이언트는 서벙에게로 데이터를 받는다.

또한 서버에서 보내온 다른 클라이언트의 영상을 받아오기 위해 ejs를 이용하였다. 
app .set ('view engine' ,'ejs')

마지막으로 uuid를 이용하여 방마다 다른 고유의 아이디를 만들 수 있도록 하였다. 
const  { v4 : uuidV4  } = require ('uuid')

app .get ('/',(req ,res )=>{
    res .redirect (`/${uuidV4 ()}`)
})
app .get ('/:room',(req ,res )=>{
    res .render ('room',{ roomId : req .params .room  })
})

이때 app.get()은 express의 함수로 라우터의 역할을 하도록 하는 아주 중요한 함수이다. ‘/’의 경로로 접속했을 때 뒤의 콜벡함수를 실행한다는 의미로, 위의 코드는 uuid를 루트 경로의 뒤에 넣어 ejs 팸플릿 안에 새로운 방을 하나 만드는 코드이다.

express,socket.io,ejs,uuid,nodemon은 npm을 통해 다운받을 수 있다.  


nodemon은 수정된 요소를 빠르게 반영하기 위해 설치하였다. 
nodemon의 경우는 package.js 파일에 들어가 스크립트 부분을 수정해 주어야 제대로 작동한다.
npm i —save-dev nodemon의 형식으로 다운받았다. 
"scripts": {
    "devStart": "nodemon server.js"
  },
npm run devStart의 형식으로 nodemon을 실행한다. 

html,css, js의 기초 정도 밖에는 모르지만 온라인 토론 중계 플랫폼 개발이라는 목표를 빨리 달성하고 싶어서 큰 틀 정도를 공부하려 한다. 하나씩 천천히 탄탄하게 공부해보자. 
