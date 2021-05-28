---
title: "create-react-app 절대경로 설정, 타입스크립트"
date: 2021-05-18T12:28:37+09:00
categories: 
- development
- rect
tags: 
- development
- front-end
keywords: 
- development
- front-end
- react
- 리액트
- cra
- 절대경로
- 타입스크립트
cover: ""
draft: false
thumbnailImage: ""
# coverImage: //d1u9biwaxjngwg.cloudfront.net/cover-image-showcase/city.jpg
metaAlignment: center
coverMeta: out
---

타입스크립트 설치 후, 

tsc init으로 tsconfig.json을 생성했다. 

그리고, 절대 경로 설정을 위해 

tsconfig.json 파일에 path 를 변경했는데 

npm start를 할 때마다 계속 tsconfig.json파일이 자동으로 변경되었다........ ㅠㅠ

원인은 CRA로 프로젝트를 만들면 내부에 있는 웹팩 설정에서 tsconfig.json을 default로 설정하기 때문....

npm run eject를 해야 웹팩 설정이 보이고, 거기서 수정해야한다...

그런데 한번 eject를 하면 React의 버전업에 대한 자동으로 다른 구성요소 및 설정이 변경되는 장점을 잃어버리게 된다

하지만 나는 eject를 하기 싫었으므로 이를 피해가기 위해 craco를 사용하였다. 

**설치**

<table style="border-collapse: collapse; width: 100%;" border="1" data-ke-align="alignLeft"><tbody><tr><td><span style="color: #333333;">$ yarn add @craco/craco</span><br><span style="color: #333333;">$ yarn add --dev craco-alias</span></td></tr></tbody></table>

tsconfig의 paths 설정을 바로 사용하기 위해[craco-alias](https://github.com/risenforces/craco-alias#migrating-from-cra-alias)도 함께 설치

**사용법**

**package.json** 파일을 수정한다. (react-script를 craco로 변경)

```
{
	...
	"scripts": {
		"start": "craco start",
		"build": "craco build",
		"test": "craco test",
		"eject": "react-scripts eject"
	},
    ...
}
```

**tsconfig.paths.json** 파일을 루트에 생성하고 paths 설정을 한다.

```
{
	"compilerOptions": {
		"baseUrl": "src",
		"paths": {
			"~/*": [
				"./*"
			],
			"@utils/*": [
				"utils/*"
			],
			"@res/*": [
				"res/*"
			],
			"@locales": [
				"locales"
			]
		}
	}
}
```

**tsconfig.json** 맨 윗 라인에 확장 옵션을 넣는다.

```
{
	"extends": "./tsconfig.paths.json",
    "compilerOptions": {
    },
    ...
}

```

**craco.config.js** 파일을 루트에 생성 후 webpack 설정을 변경하면 된다.

```
const CracoAlias = require('craco-alias');

module.exports = {
	plugins: [
		{
			plugin: CracoAlias,
			options: {
				source: 'tsconfig',
				// as you know, CRA doesn't allow to modify tsconfig's compilerOptions
				// so you should create a separate JSON file and extend tsconfig.json from it
				// and then just specify its path here:
				tsConfigPath: 'tsconfig.paths.json',
			},
		},
	],
};

```

이제 다음과 같이 사용 할 수 있다!! WOW!

```
import { useAppSettings, getAppSettings } from '~/settings';
import { containAlphabet } from '@utils/string-util';
import { useLocalization } from '@locales';

```


{{< adsense >}}