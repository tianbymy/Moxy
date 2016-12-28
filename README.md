# Moxy
[![Maven Central](https://img.shields.io/maven-central/v/com.arello-mobile/moxy.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.arello-mobile%22%20AND%20(a%3A%22moxy%22%20OR%20a%3A%22moxy-compiler%22%20OR%20a%3A%22moxy-android%22%20OR%20a%3A%22moxy-app-compat%22)) [![license](https://img.shields.io/github/license/mashape/apistatus.svg)](https://opensource.org/licenses/MIT)

Moxy is a library that help to use MVP pattern when you do the Android Application. _Without problems of lifecycle and boilerplate code!_

Main idea of using Moxy:
![schematic_using](https://habrastorage.org/files/a2e/b51/8b4/a2eb518b465a4df9b47e68794519270d.gif)
See what's happening here in the [wiki](https://github.com/Arello-Mobile/Moxy/wiki).

## Capabilities

Moxy has a few killer features on other ways:
- _Presenter_ stay alive when _Activity_ recreated(it simplify work with multithreading)
- Automatically restore all what user see when _Activity_ recreated(including dynamic content is added)
- Capability to changes of many _Views_ from one _Presenter_

## Sample

View interface
```java
public interface HelloWorldView extends MvpView {
	void showMessage(int message);
}
```
Presenter
```java
@InjectViewState
public class HelloWorldPresenter extends MvpPresenter<HelloWorldView> {
	public HelloWorldPresenter() {
		getViewState().showMessage(R.string.hello_world);
	}
}
```
View implementation
```java
public class HelloWorldActivity extends MvpAppCompatActivity implements HelloWorldView {

	@InjectPresenter
	HelloWorldPresenter mHelloWorldPresenter;

	private TextView mHelloWorldTextView;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_hello_world);

		mHelloWorldTextView = ((TextView) findViewById(R.id.activity_hello_world_text_view_message));
	}

	@Override
	public void showMessage(int message) {
		mHelloWorldTextView.setText(message);
	}
}
```

[Here](https://github.com/Arello-Mobile/Moxy/tree/master/sample-github) you can see "Github" sample application.

## Wiki
For all information check [Moxy Wiki](https://github.com/Arello-Mobile/Moxy/wiki)

## Android studio templates
In order to avoid boilerplate code creating for binding activity,fragments and its presentation part, we propose to use Android Studio templates for Moxy. 

Templates located in [/moxy-templates](https://github.com/Arello-Mobile/Moxy/tree/master/moxy-templates)

## Links
[Telegram channel (en)](https://telegram.me/moxy_mvp_library)<br />
[Telegram channel (ru)](https://telegram.me/moxy_ru)<br />
[References](https://github.com/Arello-Mobile/Moxy/wiki#references)<br />
[FAQ](https://github.com/Arello-Mobile/Moxy/wiki/FAQ)

## Integration
Base modules integration:
```groovy
dependencies {
  ...
  compile 'com.arello-mobile:moxy:1.3.3'
  provided 'com.arello-mobile:moxy-compiler:1.3.3'
}
```
If you want to see generated code, use `apt` instead of `provided` dependency type:
```groovy
dependencies {
  ...
  apt 'com.arello-mobile:moxy-compiler:1.3.3'
}
```
Note: if you use gradle plugin verion 2.2.2 and above, so you can use `annotationProcessor` instead of `apt`:
```groovy
dependencies {
  ...
  annotationProcessor 'com.arello-mobile:moxy-compiler:1.3.3'
}
```
For additional base view classes `MvpActivity` and `MvpFragment` add this:
```groovy
dependencies {
  ...
  compile 'com.arello-mobile:moxy-android:1.3.3'
}
```
If you are planing to use AppCompat, then you can use `MvpAppCompatActivity` and `MvpAppCompatFragment`. Then add this:
```groovy
dependencies {
  ...
  compile 'com.arello-mobile:moxy-app-compat:1.3.3'
  compile 'com.android.support:appcompat-v7:$support_version'
}
```
### Kotlin
If you are using kotlin, use `kapt` instead of `provided`/`apt` dependency type and set `generateStubs` property of `kapt` to `true`:
```groovy
dependencies {
  ...
  kapt 'com.arello-mobile:moxy-compiler:1.3.3'
}
kapt {
    generateStubs = true
}
```

## ProGuard
Moxy is completely without reflection! No special ProGuard rules required.

## License
```
The MIT License (MIT)

Copyright (c) 2016 Arello Mobile

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
