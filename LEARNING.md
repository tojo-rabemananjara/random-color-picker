# 20. React, Part II

## React State

```js
//Button.js
import React from 'react';

export class Button extends React.Component {
	render() {
		return (
			<button 
				className={ this.props.light ? 'light-button' : 'dark-button' }
        onClick={this.props.onClick}>
				Refresh
			</button>
		);
	}
}
```

```js
//index.js
import React from 'react';
import ReactDOM from 'react-dom';
import {Button} from './Button';

class Random extends React.Component {
  constructor(props) {
    super(props);
    this.state = { color: [9, 180, 309] };
    this.handleClick = this.handleClick.bind(this);
  }
  componentDidMount() {
    this.applyColor();
  }

  componentDidUpdate(prevProps, prevState) {
    this.applyColor();
  }

  formatColor(ary) {
    return 'rgb(' + ary.join(', ') + ')';
  }

  isLight() {
    const rgb = this.state.color;
    return rgb.reduce((a,b) => a+b) < 127 * 3;
  }

  applyColor() {
    const color = this.formatColor(this.state.color);
    document.body.style.background = color;
  }

  chooseColor() {
    const random = [];
    for (let i = 0; i < 3; i++) {
      random.push(Math.floor(Math.random()*256));
    }
    return random;
  }

  handleClick() {
    this.setState({
      color: this.chooseColor()
      });
  }

  render() {
    return (
      <div>
        <h1 className={this.isLight() ? 'white' : 'black'}>
          Your color is {this.formatColor(this.state.color)}.
        </h1>
        <Button
          light={this.isLight()}
          onClick={this.handleClick}/>
      </div>
    );
  }
}

ReactDOM.render(
  <Random />, 
  document.getElementById('app')
);
```

*   Did `npx create-react-app <app-name>` this time

*   props

*   `this.state = ...;`

*   `this.setState({...});`

*   A few things we don't really use for now at least

    *   ```
        App.test.js
        reportWebVitals.js
        setupTests.js
        ```

