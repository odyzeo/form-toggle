# @odyzeo/form-toggle

Simple toggle button Vue.js component.

<a href="https://form-toggle.durmstrangd.vercel.app/" target="_blank">Demo</a>

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
      >
          <template #checked>
              Yes
          </template>
          <template #unchecked>
              No
          </template>
</form-toggle>
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
| Property name     | Type    | Default value | Description |
| ----------------- | ------  | ------------- | ----------- |
| `value`           | Boolea  | false         | Initial state of the toggle button |
| `name`            | string  | ``            | Textarea or input `name` attribute |
| `disabled`        | boolea  | `false`       | Whether to disable toggle button |
| `speed`           | Number  | 300           | Transition time for the animation |
| `width`           | Number  | 50            | Width of the button |
| `height`          | Number  | 22            | Height of the button |
| `margin`          | Number  | 3             | Space between the switch and background border |
| `name`            | String  | undefined     | Name to attach to the generated input field |
| `falseValue`      | String  | `0`           | Value used in input value when unchecked |
| `trueValue`       | String  | `1`           | Value used in input value when checked |

### Events

| Name   | Description              |
| ---    | ---                      |
| change | Triggered whenever state of the component changes. <br>Contains: <br>`value` - state of the object <br>`srcEvent` - source click event |
| input  | Input event for v-model |

### Slots
| Name       | Description                                 |
| ---        | ---                                         |
| right      | Show custom content on the left side        |
| left       | Show custom content on the right side       |
| checked    | Text displayed inside toggle when checked   |
| unchecked  | Text displayed inside toggle when unchecked |

## Development

```
npm run serve
```

or

```bash
yarn serve
```
