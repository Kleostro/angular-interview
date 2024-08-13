
Для тестирования в Angular часто используются следующие основные инструменты и библиотеки:

1. **Jasmine**:
    
    - Jasmine — это фреймворк для написания модульных тестов на JavaScript. Он предоставляет синтаксис для написания тестов и различных утверждений (assertions).
    - Пример теста на Jasmine:
        
        ```TS
        describe('MyComponent', () => {
		  it('should have a defined component', () => {
		    expect(component).toBeDefined();
		  });
		});
		```
        
2. **Karma**:
    
    - Karma — это тестовый раннер, который запускает ваши тесты в различных браузерах. Он часто используется вместе с Jasmine для запуска модульных тестов.
    - Конфигурационный файл Karma (`karma.conf.js`):
        
        ```TS
        module.exports = function(config) {
		  config.set({
		    frameworks: ['jasmine', '@angular-devkit/build-angular'],
		    plugins: [
		      require('karma-jasmine'),
		      require('karma-chrome-launcher'),
		      require('karma-jasmine-html-reporter'),
		      require('karma-coverage-istanbul-reporter'),
		      require('@angular-devkit/build-angular/plugins/karma')
		    ],
		    client: {
		      clearContext: false // leave Jasmine Spec Runner output visible in browser
		    },
		    coverageIstanbulReporter: {
		      dir: require('path').join(__dirname, './coverage/my-app'),
		      reports: ['html', 'lcovonly', 'text-summary'],
		      fixWebpackSourcePaths: true
		    },
		    reporters: ['progress', 'kjhtml'],
		    port: 9876,
		    colors: true,
		    logLevel: config.LOG_INFO,
		    autoWatch: true,
		    browsers: ['Chrome'],
		    singleRun: false,
		    restartOnFileChange: true
		  });
		};
		```
        
3. **Protractor**:
    
    - Protractor — это фреймворк для e2e-тестирования, созданный специально для Angular приложений. Он работает поверх WebDriver и предоставляет API для написания тестов, которые взаимодействуют с вашим приложением через браузер.
    - Пример e2e-теста с Protractor:
        
        ```TS
        describe('workspace-project App', () => {
		  it('should display welcome message', () => {
		    browser.get(browser.baseUrl);
		    expect(element(by.css('app-root h1')).getText()).toEqual('Welcome to app!');
		  });
		});
		```
        

Эти инструменты и библиотеки предоставляют мощный набор возможностей для тестирования Angular приложений на различных уровнях: от отдельных модулей до полного рабочего процесса приложения.