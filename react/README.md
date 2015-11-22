# Airbnb React/JSX Style Guide

*A mostly reasonable approach to React and JSX*

将繁体字的改为简体字：  
<https://github.com/jigsawye/javascript/blob/master/react/README.md>

## Table of Contents

  1. [基本规范](#basic-rules)
  1. [命名](#naming)
  1. [声明](#declaration)
  1. [对齐](#alignment)
  1. [引号](#quotes)
  1. [空格](#spacing)
  1. [Props](#props)
  1. [括号](#parentheses)
  1. [标签](#tags)
  1. [方法](#methods)
  1. [排序](#ordering)

## 基本规范

  - 每个文件只包含一个 React 组件。
  - 总是使用 JSX 语法。
  - 请别使用 React.createElement ，除非你从一个不转换 JSX 的文件初始化。

## Class vs React.createClass

  - 使用扩展类 React.Component，除非你有一个非常好的理由才使用 mixins。

  ```javascript
  // bad
  const Listing = React.createClass({
    render() {
      return <div />;
    }
  });
  
  // good
  class Listing extends React.Component {
    render() {
      return <div />;
    }
  }
  ```

## Naming

  - **后缀名**：React 组件的后缀名请使用 jsx。
  - **文件名**：文件名请使用帕斯卡命名法。例如：ReservationCard.jsx。
  - **参考命名规范**: React 组件请使用帕斯卡命名法，组件的实例则使用驼峰式大小写：
    ```javascript
    // bad
    const reservationCard = require('./ReservationCard');

    // good
    const ReservationCard = require('./ReservationCard');

    // bad
    const ReservationItem = <ReservationCard />;

    // good
    const reservationItem = <ReservationCard />;
    ```

    **组件命名规范**：文件名须和组件名一致。所以 ReservationCard.jsx 的名称必须为 ReservationCard。但对于目录的根组件请使用 index.jsx 作为文件名，并使用目录名作为组件的名称：
    ```javascript
    // bad
    const Footer = require('./Footer/Footer.jsx')

    // bad
    const Footer = require('./Footer/index.jsx')

    // good
    const Footer = require('./Footer')
    ```


## 声明
  - 不要使用 displayName 来命名组件，请使用命名规范来命名组件。

    ```javascript
    // bad
    export default React.createClass({
      displayName: 'ReservationCard',
      // stuff goes here
    });

    // good
    export default class ReservationCard extends React.Component {
    }
    ```

## 对齐
  - JSX 语法请遵循以下的对齐风格

    ```javascript
    // bad
    <Foo superLongParam="bar"
         anotherSuperLongParam="baz" />

    // good
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />

    // 如果 props 适合放在同一行，就将它们放在同一行上
    <Foo bar="bar" />

    // 通常子元素有缩进
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    >
      <Spazz />
    </Foo>
    ```

## 引号
  - 总是在 JSX 的属性使用双引号（"），但是所有的 JS 请使用单引号。
    ```javascript
    // bad
    <Foo bar='bar' />

    // good
    <Foo bar="bar" />

    // bad
    <Foo style={{ left: "20px" }} />

    // good
    <Foo style={{ left: '20px' }} />
    ```

## 空格
  - 总是在自身结尾标签前加上一个空格。
    ```javascript
    // bad
    <Foo/>

    // very bad
    <Foo                 />

    // bad
    <Foo
     />

    // good
    <Foo />
    ```

## Props
  - 总是使用驼峰式大小写命名 prop。
    ```javascript
    // bad
    <Foo
      UserName="hello"
      phone_number={12345678}
    />

    // good
    <Foo
      userName="hello"
      phoneNumber={12345678}
    />
    ```

## 括号
  - 当 JSX 的标签有多行時请使用括号将它们包起来：
    ```javascript
    /// bad
    render() {
      return <MyComponent className="long body" foo="bar">
               <MyChild />
             </MyComponent>;
    }

    // good
    render() {
      return (
        <MyComponent className="long body" foo="bar">
          <MyChild />
        </MyComponent>
      );
    }

    // good, when single line
    render() {
      const body = <div>hello</div>;
      return <MyComponent>{body}</MyComponent>;
    }
    ```

## 标签
  - 沒有子标签時总是使用自身结尾标签。
    ```javascript
    // bad
    <Foo className="stuff"></Foo>

    // good
    <Foo className="stuff" />
    ```

  - 如果你的组件有多行属性，结尾标签请另起一行。
    ```javascript
    // bad
    <Foo
      bar="bar"
      baz="baz" />

    // good
    <Foo
      bar="bar"
      baz="baz"
    />
    ```

## 方法
  - React 组件的內部方法不要使用下划线作前缀。
    ```javascript
    // bad
    React.createClass({
      _onClickSubmit() {
        // do stuff
      }

      // other stuff
    });

    // good
    class extends React.Component {
      onClickSubmit() {
        // do stuff
      }

      // other stuff
    });
    ```

## 排序

  - 扩展类 React.Component 的排序：

  1. constructor
  1. optional static methods
  1. getChildContext
  1. componentWillMount
  1. componentDidMount
  1. componentWillReceiveProps
  1. shouldComponentUpdate
  1. componentWillUpdate
  1. componentDidUpdate
  1. componentWillUnmount
  1. *clickHandlers or eventHandlers* like onClickSubmit() or onChangeDescription()
  1. *getter methods for render* like getSelectReason() or getFooterContent()
  1. *Optional render methods* like renderNavigation() or renderProfilePicture()
  1. render

  - 如何定义 propTypes, defaultProps, contextTypes, 等...

  ```javascript
  import React, { Component, PropTypes } from 'react';
  
  const propTypes = {
    id: PropTypes.number.isRequired,
    url: PropTypes.string.isRequired,
    text: PropTypes.string,
  };
  
  const defaultProps = {
    text: 'Hello World',
  };
  
  export default class Link extends Component {
    static methodsAreOk() {
      return true;
    }
  
    render() {
      return <a href={this.props.url} data-id={this.props.id}>{this.props.text}</a>
    }
  }
  
  Link.propTypes = propTypes;
  Link.defaultProps = defaultProps;
  ```

  - React.createClass 的排序：

  1. displayName
  1. propTypes
  1. contextTypes
  1. childContextTypes
  1. mixins
  1. statics
  1. defaultProps
  1. getDefaultProps
  1. getInitialState
  1. getChildContext
  1. componentWillMount
  1. componentDidMount
  1. componentWillReceiveProps
  1. shouldComponentUpdate
  1. componentWillUpdate
  1. componentDidUpdate
  1. componentWillUnmount
  1. *clickHandlers or eventHandlers* like onClickSubmit() or onChangeDescription()
  1. *getter methods for render* like getSelectReason() or getFooterContent()
  1. *Optional render methods* like renderNavigation() or renderProfilePicture()
  1. render

**[⬆ back to top](#table-of-contents)**
