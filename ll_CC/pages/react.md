# ReactJS

## 설치 (in WebStorm)
 
 1. create-react-app npm package 설치
  - $ npm install -g create-react-app 

 2. package 설치
  - $ npm install -g babel webpack webpack-dev-server

## 프로젝트 생성
  
  1. 프로젝트 디렉토리 생성 후 해당 폴더에서 아래 명령어 실행 
   - $ npm init

  2. Dependency 및 plug-in 설치
   - $ npm install --save react react-dom
   - --save 옵션을 주면 package.json 에 추가 된다.

  3. 개발용 패키지 설치
   - $ npm install --save-dev babel-core babel-loader babel-preset-react babel-preset-es2015 webpack webpack-dev-server
   
```
	webpack 과 webpack-dev-server 가 글로벌로 이미 설치가 되어있는데, 로컬 모듈로 설치된 이유는 webpack 의 livereload와 비슷한 기능인 –hot 옵션을 사용하기 위함 입니다. 사실 상, webpack 모듈을 글로벌 패키지로서 꼭 설치 할 필요는 없습니다. 이를 설치 한 이유는 커맨드라인에서 webpack-dev-server을 바로 실행하기 위함인데, 로컬에만 설치하고 나중에 webpack 을 실행할 때는 ./node_modules/bin/webpack-dev-server –hot 이런식으로 실행 할 수 있습니다.

	 - https://velopert.com/814
```

  4. webpack 설정 (webpack.config.js)
    - webpack.config.js 파일 생성 후 아래 내용 입력

```json
	module.exports = {
	    entry: './src/index.js',

	    output: {
	        path: __dirname + '/public/',
	        filename: 'bundle.js'
	    },

	    devServer: {
	        inline: true,
	        port: 7777,
	        contentBase: __dirname + '/public/'
	    },

	    module: {
	            loaders: [
	                {
	                    test: /\.js$/,
	                    loader: 'babel-loader',
	                    exclude: /node_modules/,
	                    query: {
	                        cacheDirectory: true,
	                        presets: ['es2015', 'react']
	                    }
	                }
	            ]
	        }
	};

```


  5. npm start 명령어 실행 시 webpack-dev-server 실행하게 package.json 설정

```json
"scripts": 
{
    "start": "webpack-dev-server --hot --host 0.0.0.0"
}
```

## Webstorm 에 react 자동완성 설정
 
 1. File > Default Settings > Languages & Frameworks > JavaScript 의 JavaScript language Version React JSX 로 변경
 2. $ npm install @types/react 

## 참고 사이트
https://blog.jetbrains.com/webstorm/2015/10/working-with-reactjs-in-webstorm-coding-assistance/
https://velopert.com/