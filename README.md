# @odyzeo/form-toggle

Simple toggle button Vue.js component.

<a href="https://form-toggle-aid071pba.now.sh" target="_blank">Demo</a>

## Installation

### npm

```
npm install --save @odyzeo/form-toggle
```

### yarn

```
yarn add @odyzeo/form-toggle
```

### Import

```
import FormToggle from '@odyzeo/form-toggle';

Vue.use(FormToggle, {options})
```

Import styles or make your own.

```
import '@odyzeo/form-toggle/dist/form-toggle.css';
```

## Usage

```vue
<template>
  <div>
      <form-toggle
        v-model="checked"
      ></form-toggle>
  </div>
</template>
```

```vue
<script>
import FormToggle from '@odyzeo/form-toggle';

export default {
    name: 'App',
    components: {
        FormToggle,
    },
    data() {
        return {
            checked: true,
        };
    },
};
</script>
```

## Props

### input {Object} -  required
| Property name     | Type              | Default value | Description |
| ----------------- | ----------------- | ------------- | ----------- |
| `value`           | Boolean           | false         | Initial state of the toggle button |
| `name`            | string            | ``            | Textarea or input `name` attribute |
| `disabled`        | boolean           | `false`       | Whether to disable toggle button |
| `speed`           | Number            | 300           | Transition time for the animation |
| `width`           | Number            | 50            | Width of the button |
| `height`          | Number            | 22            | Height of the button |
| `margin`          | Number            | 3             | Space between the switch and background border |
| `name`            | String            | undefined     | Name to attach to the generated input field |

### Events

| Name   | Description              |
| ---    | ---                      |
| change | Triggered whenever state of the component changes. <br>Contains: <br>`value` - state of the object <br>`srcEvent` - source click event |
| input  | Input event for v-model |

### Slots
| Name   | Description                           |
| ---    | ---                                   |
| right  | Show custom content on the left side  |
| left   | Show custom content on the right side |

## Development

```
npm run serve
```

or

```bash
yarn serve
```
