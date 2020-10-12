# Warsztaty - Aplikacje webowe w praktyce

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Wstęp - cel warsztatów

  - podstawy poszczególnych technologii,
  - zapoznanie się z narzędziami developerskimi,
  - poznanie pojęć i teorii,
  - wzorce projektowe i dobre praktyki,
  - nauka na przykładach
  
## HTML
HTML (ang. HyperText Markup Language) – hipertekstowy język znaczników, wykorzystywany do tworzenia dokumentów hipertekstowych.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <link rel="stylesheet" href="styles.css">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <title>App title</title>
    <style>
      h1 {color:red;}
      p {color:blue;}
    </style>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
    
    <script src="yourscriptname.js"></script>
  </body>
</html>
```

### Składnia i możliwości HTML'a

https://developer.mozilla.org/en-US/docs/Web/HTML/Element
https://www.w3schools.com/html - tutaj ostroznie, czasami pojawialy sie glupoty

### Kolejnosc uruchamiania i ladowania skryptow

https://stackoverflow.com/questions/8996852/load-and-execute-order-of-scripts

### Semantyczny HTML


> Uzywanie semantycznego HTML'a ulatwia czytanie dokumentu dla developera oraz przegladarki

> `Non-semantic` - `<div>, <span>`

> `Semantic`: `<form>, <table>, <article>` - definiuja kontent

## CSS

https://pl.wikipedia.org/wiki/Kaskadowe_arkusze_styl%C3%B3w

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <link rel="stylesheet" href="styles.css">
    <title>App title</title>
    <style>
      h1 {color:red;}
      p {color:blue;}
      .my-class {
          background: red;
      }
    </style>
  </head>
  <body>
    <div class="my-class"></div>
  </body>
</html>
```

### Składnia i możliwości

https://www.w3schools.com/css/
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference#DOM-CSS_CSSOM

```css
:root {
  --main-bg-color: coral;
}

.class {
  background: var(--main-bg-color);
}

#id {
  display: flex;
  align-items: center;
}

@media (max-width: 600px) {
  #id {
    width: 100%;
  }
}

```

### Preprocesory

Dodaja nowe mozliwosci do CSS. Petle, wyrazenia warunkowe, lepsze API do zmiennych, mixiny, dziedziczenie, zagniezdzanie itp.
Jedny z najbardziej popularnych jest `SASS`.

https://sass-lang.com/documentation

```scss
@import 'styles/mixins';

@mixin col {
  display: flex;
  flex-flow: column;
}

@mixin colCenter {
  display: flex;
  flex-flow: column;
  align-items: center;
}

.navbar {
  @include row;
  grid-area: nav;
  border-bottom: 1px solid rgba($primary, 0.43);
  background: $surface;
  padding: 0 40px;

  .breadcrumbs {
    @include row;
    margin-right: auto;

    .breadcrumb {
      @include headingSmall;
      color: $primary;
      text-transform: capitalize !important;

      &:first-of-type {
        @include headingMedium;
      }

      a {
        text-decoration: none;
        color: $primary;
      }
    }

    .breadcrumbDivider {
      color: $primary;
      margin: 0 6px;

      &:last-of-type {
        display: none;
      }
    }
  }

  .divider {
    height: 30px;
    width: 1px;
    margin: 0 32px;
    background: rgba($primary, 0.43);
  }
}

```

## JavaScript

Jezyk wielo-paradygmatowy - programowanie funkcyjne, obiektowe.
Bazuje na dziedziczeniu prototypowym.
Easy to learn hard to master.

https://developer.mozilla.org/pl/docs/Web/JavaScript
https://www.w3schools.com/js/

```js
class User {
  constructor(id, name) {
    this.id = id;
    this.name = name;
    this.chatRoom = null;
  }
  
  send(message, to) {
    this.chatRoom.send(message, this, to);
  }
  
  receive(message, from) {
    if (from) {
       console.log(`Message from ${from.name} to      ${this.name}`);
    } else {
      console.log(`Global message by ${this.name}`);
    }
  }
}

class ChatRoom {
  users = {};
  
  register(...users) {
     for(let i = 0; { length } = users, i < length; i++) {
       this.users[users[i].id] = users[i];
       users[i].chatRoom = this;
     }
  }
  
  send(message, from, to) {
    if (to) {
      to.receive(message, from);
    } else {
      for(const key in this.users) {
        if (this.users[key] !== from) {
           this.users[key].receive(message);
        }
      }
    }
  }
}

const chatRoom = new ChatRoom();

const paul = new User(0, 'Paul');
const john = new User(1, 'John');
const rebecca = new User(2, 'John');

chatRoom.register(paul, john, rebecca);
                              
paul.send('Hello', john);
john.send('Hello', paul);

john.send('Hello');
```

## TypeScript

Silnik + kompilator - tak naprawde nowy jezyk.
Typescript jest opcjonalnie typowany - oznacza to, ze mozemy pisac zwykly JavaScript, a i tak bedzie on dzialac - odpowiednie ustawienia kompilatora.
Typescript jest niczym "dodatkowa warstwa abstrakcji nalozona na JS" - oznacza to tyle, ze piszemy kod innym jezyku
opartym na JS i jest on docelowo kompilowany do JS w oparciu o ustawienia kompilatora.

https://www.typescriptlang.org/

Zalety:
- podpowiedzi podczas developmentu - po zdefiniowaniu interfejsu, typu nasze IDE bedzie zdolne do podpowiadania typu zmiennych,
- bledy podczas kompilacji, a nie tylko podczas uzytkowania,
- kod bardziej odporny na bledy,
- odpada znaczna ilosc testow potrzebnych do napisania

Wady:
- moze generowac wiekszy rozmiar kodu - za kompilacje TS -> JS odpowiada kompilator i zawarty w nim algorytm,
- dodatkowy narzut pracy przy kazdej funkcjonalnosci
- nacisk na programowanie obiektowe - w swiecie FE programowanie obiektowe sie sprawdza lecz utrudnia budowanie aplikacji webowych - tych wiekszych jezeli zalezy nam na malym rozmiarze skryptow,
- pomimo definicji typow - i tak developer moze zrobic blad ktorego nie zauwazy - dalej to tylko JavaScript
- zmusza do definicji plikow z typami `index.d.ts` - jezeli jakis fragment kodu z bibliotki ich nie ma

```ts
import { Subject, fromEvent, Subscription } from 'rxjs';
import { debounceTime, map, skip, tap } from 'rxjs/operators';
import { FromEventTarget } from 'rxjs/internal/observable/fromEvent';

namespace ScrollObserver {
  export type OnEmit = (position: Position) => void;

  export interface Position {
    bottom: boolean;
  }
}

class Position implements ScrollObserver.Position {
  bottom: boolean;

  constructor(offset: number) {
    this.bottom = this._calcBottom(offset);
  }

  private _calcBottom = (offset: number) =>
    window.innerHeight + window.scrollY >= document.body.offsetHeight - offset;
}

class ScrollObserver {
  static TIME = 200;

  static OFFSET = 800;

  private _position = new Subject<Position>();

  private _position$ = this._position.asObservable();

  private _subs = new Subscription();

  constructor(
    private _target: FromEventTarget<Event>,
    private _onEmit: ScrollObserver.OnEmit,
    private _offset = ScrollObserver.OFFSET,
    private _time = ScrollObserver.TIME
  ) {
    this._subs.add(this._handleScroll());
    this._subs.add(this._handleEmit());
  }

  private _emitPosition = (position: Position) => {
    this._position.next(position);
  };

  private _toPosition = () => new Position(this._offset);

  private _handleScroll = () =>
    fromEvent(this._target, 'scroll')
      .pipe(skip(1), debounceTime(this._time), map(this._toPosition), tap(this._emitPosition))
      .subscribe();

  private _handleEmit = () => this._position$.subscribe(this._onEmit);

  unsubscribe = () => {
    this._subs.unsubscribe();
  };
}

export default ScrollObserver;

```

## Testing

Jest wiele narzedzi do testowania kodu `JS`.

 - `jest` - https://jestjs.io/
-  `react-testing-library` - https://github.com/testing-library/react-testing-library
-  `mocha` - https://mochajs.org/
-  `chai` - https://www.chaijs.com/api/bdd/
-  `enzyme` - https://enzymejs.github.io/enzyme/docs/api/
-  `karma` - https://karma-runner.github.io/latest/index.html
-  `jasmine` - https://jasmine.github.io/

```ts
import React, { useEffect, useState } from 'react';
import { fireEvent, render, waitFor, screen } from '@testing-library/react';

import { ScrollObserver } from '..';

describe('ScrollObserver', () => {
  const _BOTTOM_LABEL = 'Bottom';

  const scrollWindow = (scrollY: number, innerHeight: number) => {
    fireEvent.scroll(window, { target: { scrollY, innerHeight } });
  };

  const ComponentStub = ({ offset = ScrollObserver.OFFSET, time = ScrollObserver.TIME }) => {
    const [position, setPosition] = useState<ScrollObserver.Position>(null);

    useEffect(() => {
      const sub = new ScrollObserver(window, setPosition, offset, time);

      return () => {
        sub.unsubscribe();
      };
    }, []);

    return <div>{position ? (position.bottom ? _BOTTOM_LABEL : '') : ''}</div>;
  };

  describe('detects when it reaches the bottom edge with', () => {
    const mockBodyOffsetHeight = (value: number) => {
      Object.defineProperty(document.body, 'offsetHeight', {
        writable: true,
        value
      });
    };

    beforeEach(() => {
      mockBodyOffsetHeight(3769);
    });

    afterEach(() => {
      mockBodyOffsetHeight(0);
    });

    it('default offset', async () => {
      render(<ComponentStub />);

      scrollWindow(2200, 939);
      scrollWindow(2200, 939);

      await waitFor(() => screen.getByText(_BOTTOM_LABEL));

      expect(screen.getByText(_BOTTOM_LABEL)).toBeInTheDocument();
    });

    it('custom offset', async () => {
      render(<ComponentStub offset={0} />);

      scrollWindow(2900, 939);
      scrollWindow(2900, 939);

      await waitFor(() => screen.getByText(_BOTTOM_LABEL));

      expect(screen.getByText(_BOTTOM_LABEL)).toBeInTheDocument();
    });
  });
});

```

## Frameworki SPA - po co powstaja ?

- React - https://pl.reactjs.org/docs/getting-started.html
- Angular - https://angular.io/docs
- Vue - https://vuejs.org/v2/guide/

### Static pages
https://en.wikipedia.org/wiki/Static_web_page
Przyklad strony internetowej - blog.

Blog to zwykla strona statyczna - posiada kilkanascie dokumentow HTML z podlinkowanymi skryptami, plikami css oraz innymi assetami. Nie jest to aplikacja webowa - i nie ma potrzeby zeby nia byla.
- Rozwiazanie to daje dobre SEO - wysokie pozycjonowanie ze wzgledu na statyczny kontent strony ktory moze byc latwo analizowany przez boty,
- Jest tez bardzo szybkie pod katem wyswietlania tresci,
- Ciezko implementowac jest dynamiczne rzeczy - typu komentarze pod sekcjami, jakis admin panel ewentualnie itd.

### SSR
https://medium.com/@baphemot/whats-server-side-rendering-and-do-i-need-it-cb42dc059b38
Przyklad platformy - Allegro.

Allegro jest platforma stawiajaca na mozliwosc przegladania oferty produktow itp oraz na poszczegolne interakcje - np formularze, leniwe ladowanie, logownaie, rejestracja itp.
Uzycie do tego stron statycznych byloby praktycznie niewykonalne. Znacznie latwiej jest generowac widok dynamicznie po stronie serwera - dorzucajac potrzebne dane z backendu oraz skrypty obslugujace formularze dodatkowe interakcje.
- Rozwiazanie to daje dobre SOE - strony sa generowane dynamicznie po stronie serwera wiec boty moga przeanalizowac ich tresc,
- Szybkosc przy malej liczbe userow,
- Im wiecej userow tym gorszy performance - potrzebna dobra architektura serwerowa,
- Duplikacja kodu

### SPA
https://en.wikipedia.org/wiki/Single-page_application
Przyklad aplikacji - panel admina

Aplikacja nie musi miec wsparcia SEO - owszem widoczna w internecie, ale tylko i wylacznie jako calosc, a nie to co sie znajduje wewnatrz. Pelno formularzy, tabel, wykresow itp.

- Dlugi czas inicjalnego ladowania,
- Zyskuje po zaladowaniu - wygrywa pod wzgledem szybkosci wyswietlania tresci - dzieki cachowaniu plikow statycznych,
- Lepszy UX - strona nie znika - kontent "wewnatrz" sie zmienia,
- Slabe SEO

### React vs Angular vs Vue

- `React` - VirtualDOM - widok zmienia sie gdy zmieniamy obiekt state, podejscie pure functions i niemutowalnosci. Wszystko jest komponentem, Uni-directional-data-flow, latwy prog wejscia - hard to master, totalna dowolnosc - brak narzucania praktyk czy konwencji poza podstawowymi,
- `Angular` - IncrementalDOM - widok zmienia sie wtedy zmieni sie wartosci w instancji klasy komponentu - mozliwosc manualnej zmiany - wykrycia zmian i renderu, duzy prog wejscia - easy to master, potezne CLI i masa gotowych rozwiazan. Korzystana z DI, programowania reaktywnego i domyslnie uzywa TypeScript'a - rozwiazanie do apek enterprise, duzo boiletplate
`Vue` - VirtualDOM - podobne dzialanie do Angulara, lekki, szybki, najblizszy czystemu JS,

- Roznia sie algorytmem obslugujacym proces podmiany kontentu na stronie za pomoca JS,
- Rozmiarem,
- Sposobem dzialania oraz skladnia

Ktory wybrac ?

- Do aplikacji ogromnych, skomplikowanych biznesowo - Angular - pozwala na tworzenie rozwiazan w szybki sposob dzieki CLI oraz w miare bezpiecznych dzieki TS + RxJs pod katem potencjalnych bugow. Latwosc tworzenia projektu 1 komenda i dodwanie komponentow za pomoca kolejnych. Dodanie PW'a to banal czy SSR takze. 
- Do aplikacji kazdych - React - pomimo, ze nie narzuca zadnego flow - to korzystajac z Redux'a, TypeScript czy RxJs'a jestesmy wstanie pisac kod bardzo bezpieczny. Dodatkowo latwosc konfiguracji wszystkiego od zera oraz idealne wsparcie dla Ts'a czasami powoduja ze lepiej jest pisac w React niz w Angularze. Szybki, dobry mechanizm Hot Realoading. Dzieki JSX doskonala definicja typow.
- Do aplikacji malych i srednich - Vue - posiada wlasne ClI rowniez, malo boilerplate, trudnosci z typescript, slabe definicje typow.

## Webpack

https://webpack.js.org/concepts/


```json
{
  "name": "react-templates",
  "version": "1.0.0",
  "description": "",
  "scripts": {
    "start": "webpack-dev-server --hot --progress --mode development",
    "build": "webpack --mode production",
    "build:run:prod": "webpack-dev-server --progress --mode production",
    "test": "jest",
    "test-coverage": "jest --coverage",
    "test-watch": "jest --watch",
    "test-watch-silent": "jest --watch --silent"
  },
  "author": "Adrian Połubiński",
  "license": "ISC",
  "devDependencies": {
    "@babel/core": "^7.8.3",
    "@babel/preset-env": "^7.8.3",
    "@babel/preset-react": "^7.8.3",
    "@testing-library/jest-dom": "^5.11.3",
    "@testing-library/react": "^10.4.9",
    "@testing-library/react-hooks": "^3.2.1",
    "@types/jest": "^25.1.1",
    "@types/ramda": "^0.27.11",
    "@types/react": "^16.9.18",
    "@types/react-dom": "^16.9.5",
    "@types/react-router": "^5.1.4",
    "@types/react-router-dom": "^5.1.3",
    "@types/react-window": "^1.8.2",
    "awesome-typescript-loader": "^5.2.1",
    "babel-jest": "^25.1.0",
    "babel-loader": "^8.0.6",
    "copy-webpack-plugin": "^5.1.1",
    "css-loader": "^3.4.2",
    "css-modules-typescript-loader": "^4.0.0",
    "file-loader": "^5.0.2",
    "html-loader": "^0.5.5",
    "html-webpack-plugin": "^3.2.0",
    "identity-obj-proxy": "^3.0.0",
    "interpolate-html-plugin": "^3.0.0",
    "jest": "^25.1.0",
    "mini-css-extract-plugin": "^0.9.0",
    "node-sass": "^4.13.1",
    "react-test-renderer": "^16.12.0",
    "sass-loader": "^8.0.2",
    "style-loader": "^1.1.3",
    "ts-jest": "^25.2.0",
    "tslint": "^6.0.0",
    "typedoc": "^0.16.9",
    "typescript": "^3.9.5",
    "webpack": "^4.41.5",
    "webpack-bundle-analyzer": "^3.6.0",
    "webpack-cli": "^3.3.10",
    "webpack-dev-server": "^3.10.1"
  },
  "dependencies": {
    "@material-ui/core": "^4.9.7",
    "@material-ui/icons": "^4.9.1",
    "axios": "^0.19.2",
    "is-github-url": "^1.2.2",
    "ramda": "^0.27.0",
    "react": "^16.13.1",
    "react-dom": "^16.13.1",
    "react-router": "^5.1.2",
    "react-router-dom": "^5.1.2",
    "react-window": "^1.8.5",
    "rxjs": "^6.6.2",
    "webfontloader": "^1.6.28"
  }
}

```

```js
const path = require('path');

const DefinePlugin = require('webpack').DefinePlugin;
const TsConfigPathsPlugin = require('awesome-typescript-loader').TsConfigPathsPlugin;
const HtmlWebPackPlugin = require('html-webpack-plugin');
const InterpolateHtmlPlugin = require('interpolate-html-plugin');
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;
const CopyPlugin = require('copy-webpack-plugin');

module.exports = (env, { mode }) => {
  const [DEV, PROD] = ['development', 'production'];

  console.log(`App is running in ${mode} mode`);

  const config = {
    mode,

    devtool: mode === PROD ? false : 'inline-source-map',

    entry: path.resolve(__dirname, 'src/index.tsx'),

    resolve: {
      extensions: ['.ts', '.tsx', '.js'],
      alias: {
        styles: path.resolve(__dirname, 'src/styles')
      },
      plugins: [new TsConfigPathsPlugin()]
    },

    output: {
      path: __dirname + '/dist',
      filename: '[name].[hash].js',
      publicPath: '/'
    },

    module: {
      rules: [
        {
          test: /\.tsx?$/,
          loader: 'awesome-typescript-loader'
        },
        {
          test: /\.scss$/,
          exclude: path.resolve(__dirname, 'src/styles/'),
          use: [
            'style-loader',
            'css-modules-typescript-loader',
            {
              loader: 'css-loader',
              options: {
                sourceMap: true,
                modules: {
                  localIdentName: '[local]___[hash:base64:5]'
                }
              }
            },
            'sass-loader'
          ]
        },
        {
          test: /\.scss$/,
          include: path.resolve(__dirname, 'src/styles/'),
          use: ['style-loader', 'css-loader', 'sass-loader']
        },
        {
          test: /\.html$/,
          use: ['html-loader']
        },
        {
          test: /\.(png|svg|jpg|jpeg|gif|ico)$/,
          exclude: /node_modules/,
          use: ['file-loader?name=[name].[ext]']
        },
        {
          test: /\.(config)$/,
          use: {
            loader: 'file-loader',
            options: {
              name: '[name].[ext]'
            }
          }
        }
      ]
    },

    plugins: [
      new HtmlWebPackPlugin({
        template: './public/index.html',
        favicon: './public/favicon.ico',
        inject: 'body',
        hash: true
      }),
      new InterpolateHtmlPlugin({
        PUBLIC_URL: 'public'
      }),
      new DefinePlugin({
        __IMAGES_PATH__: mode === DEV ? "'public/images'" : "'images'",
        __CORE_API_PATH__: "'https://pillar-api-dev.azurewebsites.net/api/'"
        // TODO UNCOMMENT THIS AFTER FE PROD ENVIRONMENT READY
        // mode === DEV
        //   ? "'https://pillar-api-dev.azurewebsites.net/api/'"
        //   : "'https://pillar-api.azurewebsites.net/api/'"
      })
    ],

    devServer: {
      historyApiFallback: true,
      port: 3000
    }
  };

  if (mode === PROD) {
    config.optimization = {
      runtimeChunk: 'single',
      splitChunks: {
        chunks: 'all',
        maxInitialRequests: Infinity,
        cacheGroups: {
          default: false, // Removes default config

          vendor: {
            test: /[\\/]node_modules[\\/]/,
            name(module) {
              // We creating here node_modules single package name
              return `npm.${module.context
                .match(/[\\/]node_modules[\\/](.*?)([\\/]|$)/)[1]
                .replace('@', '')}`;
            },
            minSize: 0
          }
        }
      }
    };

    config.plugins.push(new CopyPlugin([{ from: 'public', ignore: ['index.html'] }]));
  }

  if (mode !== PROD) {
    config.plugins.push(
      new BundleAnalyzerPlugin({
        openAnalyzer: false
      })
    );
  }

  return config;
};

```

## React

https://pl.reactjs.org/docs/getting-started.html

- Bazuje na architekturze komponentow. Wszystko jest komponentem - kwestia tylko czy klasowym czy funkcyjnym.
- Przyjelo sie rozdzielac komponenty na smart/dumb czy logiczne/prezentacyjne.
- Widok zostaje zaktualizowany tylko po uzyciu setState, forceUpdate albo hooka useState czy useReducer.
- Wykorzystuje VirtualDOM,
- Nowy stan to jak nowe zdjecie,
- Najkosztowniejsza operacja do detekcja zmian w drzewie VDOM i naniesienie ich na prawdziwy DOM,
- Pozwala na wykonywanie efektow ubocznych podczas cyklow zycia komponentow

```ts
import React, { createContext, ReactNode, useContext } from 'react';

import { getTechnologies, Technology } from 'core/api';

namespace TechnologiesProvider {
  export interface State {
    loading: boolean;
    error: string;
    technologies: Technology[];
    getTechnologies?(query?: string): void;
  }

  export interface Props {
    children: ReactNode;
  }
}

const STATE: TechnologiesProvider.State = {
  loading: true,
  error: '',
  technologies: []
};

const Context = createContext(STATE);

class Provider extends React.Component<TechnologiesProvider.Props, typeof STATE> {
  getTechnologies = async (query = '') => {
    if (!this.state.loading) {
      this.setState({ ...STATE });
    }

    try {
      const technologies = await getTechnologies(query);
      this.setState({ ...STATE, loading: false, technologies });
    } catch (error) {
      this.setState({ ...STATE, loading: false, error });
    }
  };

  readonly state: typeof STATE = {
    ...STATE,
    getTechnologies: this.getTechnologies
  };

  render = () => <Context.Provider value={this.state}>{this.props.children}</Context.Provider>;
}

const TechnologiesProvider = Provider;

export const useTechnologiesProvider = () => {
  const context = useContext(Context);

  return context;
};

export default TechnologiesProvider;
```

```ts
import React, { useCallback, useEffect } from 'react';
import { useHistory } from 'react-router';

import { Button } from '@material-ui/core';
import CodeIcon from '@material-ui/icons/Code';
import SearchIcon from '@material-ui/icons/Search';
import PlaylistAddIcon from '@material-ui/icons/PlaylistAdd';

import { SelectBase } from 'ui';

import { Form, useQueryParams, Url, isJSONString } from 'utils';

import { PatternsSelect, TechnologiesSelect } from 'shared/components';

import ControlButton from './control-button';

import csx from './TemplatesSearch.scss';

namespace TemplatesSearch {
  export interface Props {
    className?: string;
    pathname: string;
  }
}

const [QUERY, PATTERNS, TECHNOLOGIES] = [0, 1, 2];

const parseFromString = (str: string) =>
  isJSONString(str)
    ? (JSON.parse(str) as string[]).reduce((prev, id) => ({ ...prev, [id]: true }), {})
    : {};

const CONFIG: Form.Config = [
  { label: 'Query', value: '' },
  { label: 'Patterns', value: {} },
  {
    label: 'Technologies',
    value: {}
  }
];

const TemplatesSearch = ({ className, pathname }: TemplatesSearch.Props) => {
  const { location, push } = useHistory();

  const [query, patternsIds, technologiesIds] = useQueryParams(
    'query',
    'patternsIds',
    'technologiesIds'
  );

  const [{ fields }, change, directChange, submit] = Form.useManager(CONFIG);

  const handlePatternSelect: SelectBase.OnSelect = useCallback(
    (dataIdx, value) => {
      directChange([PATTERNS], [{ ...fields[PATTERNS].value, [dataIdx]: value }]);
    },
    [fields]
  );

  const handleTechnologySelect: SelectBase.OnSelect = useCallback(
    (dataIdx, value) => {
      directChange([TECHNOLOGIES], [{ ...fields[TECHNOLOGIES].value, [dataIdx]: value }]);
    },
    [fields]
  );

  const handleSubmit = useCallback(
    (e: Form.Events.Submit) => {
      const invalid = submit(e);

      if (invalid) {
        return;
      }

      const [{ value: query }, { value: patternsIds }, { value: technologiesIds }] = fields;

      const search = Url(location)
        .swap('technologiesIds', SelectBase.getSelected(technologiesIds))
        .swap('patternsIds', SelectBase.getSelected(patternsIds))
        .swap('query', query)
        .delete('page')
        .search();

      push(`${pathname}?${search}`);
    },
    [fields, location]
  );

  useEffect(() => {
    directChange(
      [QUERY, PATTERNS, TECHNOLOGIES],
      [query, parseFromString(patternsIds), parseFromString(technologiesIds)]
    );
  }, [query, patternsIds, technologiesIds]);

  return (
    <form className={`${csx.templatesSearch} ${className}`} onSubmit={handleSubmit}>
      <input
        data-idx={QUERY}
        placeholder="Find your template..."
        className={csx.input}
        value={fields[QUERY].value}
        onChange={change}
      />

      <PatternsSelect value={fields[PATTERNS].value} onSelect={handlePatternSelect}>
        <ControlButton value={fields[PATTERNS].value}>
          <PlaylistAddIcon />
        </ControlButton>
      </PatternsSelect>

      <TechnologiesSelect value={fields[TECHNOLOGIES].value} onSelect={handleTechnologySelect}>
        <ControlButton value={fields[TECHNOLOGIES].value}>
          <CodeIcon />
        </ControlButton>
      </TechnologiesSelect>

      <Button type="submit" className={csx.confirmSearchBtn}>
        <SearchIcon />
      </Button>
    </form>
  );
};

export default TemplatesSearch;
```

```ts
import React, { forwardRef } from 'react';

import { Button as MuiButton, IconButton as MuiIconButton } from '@material-ui/core';

import csx from './Button.scss';

namespace Button {
  export interface Props
    extends React.DetailedHTMLProps<
      React.ButtonHTMLAttributes<HTMLButtonElement>,
      HTMLButtonElement
    > {
    children: React.ReactNode;
    variant?: 'default' | 'icon';
    theme?: 'primaryDark' | 'primaryTransparent' | 'danger';
  }
}

const Button = forwardRef(
  ({ children, variant = 'default', theme = 'primaryDark', ...btnProps }: Button.Props, ref) => {
    if (variant === 'icon') {
      return (
        <MuiIconButton
          {...(btnProps as any)}
          classes={{ root: `${csx.iconButton} ${csx[theme]}` }}
          ref={ref}
        >
          {children}
        </MuiIconButton>
      );
    }

    return (
      <MuiButton {...(btnProps as any)} classes={{ root: `${csx.button} ${csx[theme]}` }} ref={ref}>
        {children}
      </MuiButton>
    );
  }
);

export default Button;

```

## NodeJS
https://nodejs.org/en/
Sklada sie z warsty JS'a wykorzystujacej silnik V8 do interpretowania, kompilacji oraz biblioteke libuv - do korzystania z protokolow sieciowych, systemu plikow, operacji wejscia/wyjscia, szyfrowania itp.

Node wykorzystuje V8 wiec korzysta z mechanizmu Event Loop. Jest jedno watkowy i wykonujac skomplikowane operacje mozemy zablokowac watek. Wszystko co jest skomplikowane powinno byc wykonywane za pomoca Native Addons - piszemy kod w C++ wielowatkowy a Node odbiera tylko wynik - interpretuje to jako operacje asynchroniczna - np strzal do serwera.

## Express

https://expressjs.com/
Framework do Node'a - cos jak jQuery dla Js'a. Ulatwia prace z Node'm i redukuje boilerplate.
