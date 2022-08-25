# eslint-plugin-jsx-a11y
[eslint-plugin-jsx-a11y](https://www.npmjs.com/package/eslint-plugin-jsx-a11y) 적용을 위해 규칙을 한국어로 정리

## alt-text
사용자에게 의미있는 정보를 전달하는 대체 텍스트가 있어야함

```JSON
{
  "rules": {
    "jsx-a11y/alt-text": [ 2, {
      "elements": [ "img", "object", "area", "input[type=\"image\"]" ], // 검사대상이 되는 요소들을 작성. 요소를 삭제하면 검사대상에서 제외됨
      "img": ["Image"], //JSX 컴포넌트 지정 가능
      "object": ["Object"],
      "area": ["Area"],
      "input[type=\"image\"]": ["InputImage"]
    }],
  }
}
```
***

## anchor-ambiguous-text
anchor 텍스트는 여기를 클릭, 여기, 링크 등의 모호한 말을 사용하지 않음   
words 옵션으로 검사대상인 단어들을 설정할 수 있음

```JSON
{
  "rules": {
    "jsx-a11y/anchor-ambiguous-text": [2, {
      "words": ["click this"] //검사 대상 단어 설정
    }],
  }
}
```
***

## anchor-has-content
모든 anchor는 (보조기기가) 접근가능한 콘텐츠를 포함해야 함

```JSON
{
  "rules": {
    "jsx-a11y/anchor-has-content": [ 2, {
      "components": [ "Anchor" ] //JSX 컴포넌트 지정 가능
    }]
  }
}
```
***

## anchor-is-valid
모든 anchor는 유효하고 키보드 접근이 가능한 요소여야 함   
a태그 에는 href 필수이며 유효한 URL이 있어야함   
a태그 와 button 태그는 용도에 맞게 사용할 것   

```JSON
{
  "rules": {
    "jsx-a11y/anchor-is-valid": [
      "error",
      {
        "components": ["Link"],
        "specialLink": ["hrefLeft", "hrefRight"],
        "aspects": ["noHref", "invalidHref", "preferButton"]
      }
    ]
  }
}
```
### aspects의 하위 규칙

* noHref: href 속성 여부 확인
* invalidHref: href값이 유효한 값인지 확인
* preferButton: 앵커가 버튼으로 사용되었는지 확인
***

## aria-activedescendant-has-tabindex
aria-activedescendant가 있는 요소를 탭 할 수 있음 (고유한 tabIndex가 0이거나 tabIndex속성으로 0을 지정해야함)   
 
```
옵션 없음 
```
***

## aria-props
모든 aria-* 속성은 유효해야함 (오탈자나 잘못된 속성을 사용했는지 검사)   

```
옵션 없음 
```
***

## aria-proptypes
ARIA 상태 및 속성 값이 유효해야함 (올바른 속성값을 사용했는지 검사)   

```
옵션 없음 
```
***
 
## aria-role
ARIA 역할은 유효한, 비추상(명확한) 역할이어야 함   

```JSON
{
  "rules": {
    "jsx-a11y/aria-role": [ 2, {
      "allowedInvalidRoles": ["text"],
      "ignoreNonDOM": true
    }],
  }
}
```
* allowedInvalidRoles: role="text"같이 비표준 속성을 사용해야 하는 경우 검사에서 허용해야하는 문자열
* ignoreNonDOM: 개발자가 만든 구성요소가 선택되었는지 여부를 결정
***

## aria-unsupported-elements
meta, html, script 태그와 같이 ARIA 역할, 상태 및 속성을 지원하지 않는 요소에 사용하지 않아야함   

```
옵션 없음 
```
***

## autocomplete-valid
자동 완성 속성을 입력 필드에 적합하게 사용해야함   

```JSON
{
  "rules": {
    "jsx-a11y/autocomplete-valid": [ 2, {
      "inputComponents": ["Input", "FormField"] //JSX 컴포넌트 지정 가능
    }],
  }
}
```
***

## click-events-have-key-events
클릭 가능한 요소에는 최소한 하나의 키보드 이벤트가 있어야함 (onKeyUp, onKeyDown, onKeyPress)   
button 태그 같은 대화형 요소나 aria-hidden="true"등 숨겨진 요소에는 적용 안됨   

```
옵션 없음 
```
***

## heading-has-content
제목(h1, h2 등) 요소에 보조기기가 인식 가능한 콘텐츠가 포함되어 있어야함   

```JSON
{
  "rules": {
    "jsx-a11y/heading-has-content": [ 2, {
      "components": [ "MyHeading" ], //JSX 컴포넌트 지정 가능
    }],
  }
}
```
***

## html-has-lang
html 태그에 lang 속성이 있어야함   

```
옵션 없음 
```
***

## iframe-has-title
iframe 태그에는 title 속성으로 제목이 제공되어야 함   

```
옵션 없음 
```
***

## img-redundant-alt
img 태그의 al t속성에 "이미지", "사진" 과 같은 텍스트가 포함되어 있지 않아야함 (불필요하거나 중복의 이유로)   
* 한국어 (이미지, 사진, 그림 등등) 인식이 안되는 것 같음

```JSON
{
  "rules": {
    "jsx-a11y/img-redundant-alt": [ 2, {
      "components": [ "Image" ], //JSX 컴포넌트 지정 가능
      "words": [ "Bild", "Foto" ], //검사 대상 단어 설정
    }],
  }
}
```
***

## Interactive-supports-focus
onClick과 같이 상호 작용 가능한 요소에는 포커스가 가능해야 함   

* 권장모드 기본 옵션
```JSON
{
  "rules": {
    "jsx-a11y/interactive-supports-focus": ["error", {
      //role 속성으로 초점 대상 지정
      "tabbable": ["button", "checkbox", "link", "searchbox", "spinbutton", "switch", "textbox"]
    }],
  }
}
```
***

## label-has-associated-control
label 태그에 텍스트 레이블 및 관련 컨트롤이 있는 지 확인 함   

```JSON
{
  "rules": {
    "jsx-a11y/label-has-associated-control": [ 2, {
      "labelComponents": ["CustomLabel"],
      "labelAttributes": ["inputLabel"],
      "controlComponents": ["CustomInput"],
      "assert": "both", // options: 'htmlFor', 'nesting', 'both', 'either'.
      "depth": 3, // default 2, max 25
    }],
  }
}
```
***

## lang
lang 속성에 바른 값이 있는지 확인 (IETF's BCP 47에 정의된)   

```
옵션 없음 
```
***

## media-has-caption
audio 및 video 태그에 캡션에 대한 track이 있어야 함   

```JSON
{
  "rules": {
    "jsx-a11y/media-has-caption": [ 2, {
      "audio": [ "Audio" ],
      "video": [ "Video" ],
      "track": [ "Track" ],
    }],
  }
}
```
***

## mouse-events-have-key-events
키보드 전용 사용자를 위해 onMouseOver/onMouseOut과 함께 onFocus/onBlur를 제공해야 함   

```
옵션 없음 
```
***

## no-access-key
요소에 accessKey 속성을 사용하지 않아야함 (스크린리더의 단축키나 명령과 충돌할 수 있음)   

```
옵션 없음 
```
***

## no-autofocus
AutoFocus 속성을 사용하지 않아야함   

```JSON
{
  "rules": {
    "jsx-a11y/no-autofocus": [ 2, {
      "ignoreNonDOM": true // 사용자가 만든 구성 요소의 확인여부
    }],
  }
}

```
***

## no-distracting-elements
marquee, blink 태그와 같은 시각적으로 산만한 요소를 사용하지 않아야함   
권장모드/엄격모드에 설정되어 있지 않아 별도로 설정해야함   

```JSON
{
  "rules": {
    "jsx-a11y/no-distracting-elements": [ 2, {
      "elements": [ "marquee", "blink" ],
    }],
  }
}
```
***

## no-interactive-element-to-noninteractive-role
WAI-ARIA Role은 대화형 요소를 비대화용 요소의 역할로 변환하는데 사용하지 않아야함   
옵션을 통해 요소에 허용되는 역할을 지정할 수 있음   

* 권장모드 기본 옵션   
```JSON
{
  "rules": {
    "no-interactive-element-to-noninteractive-role": ["error", {
      "tr": ["none", "presentation"], // html 요소로 지정하고 값은 Role
      "canvas": ["img"]
    }],
  }
}
```
***
 
## no-non-interactive-element-interactions
비대화형 요소나 역할에 마우스 또는 키보드 이벤트를 할당하지 않아야함   
옵션을 통해 허용 범위를 추가하거나 삭제할 수 있음   
* 권장모드 기본 옵션   

```JSON
{
  "rules": {
    "jsx-a11y/no-noninteractive-element-interactions": ["error", {
      "handlers": ["onClick", "onError", "onLoad", "onMouseDown", "onMouseUp", "onKeyPress", "onKeyDown", "onKeyUp"],
      "alert": ["onKeyUp", "onKeyDown", "onKeyPress"],
      "body": ["onError", "onLoad"],
      "dialog": ["onKeyUp", "onKeyDown", "onKeyPress"],
      "iframe": ["onError", "onLoad"],
      "img": ["onError", "onLoad"]
    }],
  }
}
```
***

## no-non-interactive-element-to-interactive-role
WAI-ARIA Role은 비대화형 요소를 대화형 요소의 역할로 변환하는데 사용하지 않아야함   
옵션을 통해 요소에 허용되는 역할을 지정할 수 있음   
* 권장모드 기본 옵션

```JSON
{
  "rules": {
    "jsx-a11y/no-noninteractive-element-to-interactive-role": ["error", {
      "ul": ["listbox", "menu", "menubar", "radiogroup", "tablist", "tree", "treegrid"], // html 요소로 지정하고 값은 Role
      "ol": ["listbox", "menu", "menubar", "radiogroup", "tablist", "tree", "treegrid"],
      "li": ["menuitem", "option", "row", "tab", "treeitem"],
      "table": ["grid"],
      "td": ["gridcell"],
      "fieldset": ["radiogroup", "presentation"]
    }],
  }
}
```
***

## no-non-interactive-tabindex 
tabIndex는 대화형 요소에 대해서만 선언되어야함   
* 권장모드 기본 옵션   

```JSON
{
  "rules": {
    "jsx-a11y/no-noninteractive-tabindex": ["error", {
      "tags": [],
      "roles": ["tabpanel"],
      "allowExpressionValues": true,
    }],
  }
}
```
***

## no-redundant-roles
ARIA의 role은 요소의 기본적인 역할과 중복되지 않아야함   
옵션을 통해 요소에 허용되는 역할 값을 지정할 수 있음   

```JSON
{
  "rules": {
    "jsx-a11y/no-redundant-roles": ["error", {
      "nav": ["navigation"],
    }],
  }
}
```
***

## no-static-element-interactions
div와 같이 비대화형 가시적 요소에 마우스나 키보드 이벤트가 있으면 role 속성을 사용하여 역할을 나타내야함   
옵션을 통해 적용 이벤트를 조정 할 수 있음   
* 권장모드 기본 옵션   

```JSON
{
  "rules": {
    "jsx-a11y/no-static-element-interactions": ["error", {
      "allowExpressionValues": true, // 표현식을 통해 role 속성을 할당할 경우 사용
      "handlers": ["onClick", "onMouseDown", "onMouseUp", "onKeyPress", "onKeyDown", "onKeyUp"]
    }],
  }
}
```
***

## role-has-required-aria-props
ARIA role 이 있는 요소에는 해당 role에 필요한 모든 속성이 있어야 함   

```
옵션 없음
```
***

## role-supports-aria-props
명시적 또는 암시적 역할이 정의된 요소에는 해당 역할에서 지원하는 aria-* 속성만 포함되도록함   

```
옵션 없음
```
***

## scope
scope 속성은 <th> 요소에만 사용함   
```
옵션 없음
```
***

## tabindex-no-positive
tabIndex의 값은 0보다 크지 않아야함   
```
옵션 없음
```
