# @tillhub/vue-sidebar [![CircleCI](https://circleci.com/gh/tillhub/vue-sidebar/tree/master.svg?style=svg)](https://circleci.com/gh/tillhub/vue-sidebar/tree/master)
> Vue search input with dropdown for more filters


## Install

```bash
npm install --save @tillhub/vue-sidebar
```

## Usage

Please see example folder for complete code example.

To see the example in action:

```bash
npm run serve
```

The sidebar is based on ElementUI's original `Dialog` code. All properties/events except `fullscreen` are still available. Please read ElementUI's documentation for more information: http://element.eleme.io/#/en-US/component/dialog

### Added properties

| Attribute        | Type    | Required | Example           | Default | Description                                                         |
|------------------|---------|----------|-------------------|---------|---------------------------------------------------------|
| bottom           | string  | no       | "15vh"            | "0px"   | sets bottom padding, similar to `top` prop              |
| position         | string  | no       | "left" or "right" | "right" | fixes sidebar to the left or right edge of the viewport |
| hide-title       | boolean | no       | "true" or "false" | "false" | completely removes the dialog header                    |
| padding          | string  | no       | "10px 3px"        | "0"     | sets the padding of the dialog body                     |

## License

MIT © [Endebert](https://github.com/Endebert)
