# 🕉 @feelinglovelynow/svelte-modal


## 💎 Install
```bash
pnpm add @feelinglovelynow/svelte-modal
pnpm add @feelinglovelynow/global-style # Only necessary if prerequisite css below is not present
```


## 🙏 Description
Simple modal component for Svelte or Sveltekit applications that includes a showModal function, hideModal function and onHideModal callback


## 💚 Properties
```ts
export let header: string = ''
export let onHideModal: () => void = () => {}
```


## 💛 Prerequisite CSS
Requires [@feelinglovelynow/global-style](https://github.com/feelinglovelynow/global-style) or add this css to your site
```css
@keyframes fln__fade-in-from-above {
  0% {
    opacity: 0;
    transform: translateY(-9rem);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fln__fade-out-and-slide-up {
  0% {
    opacity: 1;
    transform: translateY(0);
  }
  100% {
    opacity: 0;
    transform: translateY(-9rem);
  }
}

html { /* Helps w/ rem, can still look good w/o just set rem/px as desired: https://stackoverflow.com/questions/59920538  */
  font-size: 62.5%;
}
```


## 🧡 Example
```svelte
<script lang="ts">
  import { Modal, type ShowModal, type HideModal, type OnModalHide } from '@feelinglovelynow/svelte-modal'

  let showModal: ShowModal
  let hideModal: HideModal

  const onHideModal = (() => {
    console.log('bye modal')
  }) satisfies OnModalHide

  function bind (e: CustomEvent) {
    showModal = e.detail.showModal
    hideModal = e.detail.hideModal
  }
</script>


<button on:click={ showModal }>Show Modal</button>

<Modal header="Header" on:functions={ bind } { onHideModal }>
  <div>Lorem ipsum</div>
  <button on:click={ hideModal }>Hide Modal</button>
</Modal>
```


## ❤️ Add custom styling
```scss
.fln__modal-backdrop {

}

.fln__modal {

  &__header {

    &__text {

    }

    &__close {

    }
  }

  &__body {

  }
}
```


## 🎁 All our NPM Packages
* [@feelinglovelynow/env-write](https://github.com/feelinglovelynow/env-write)
* [@feelinglovelynow/get-form-entries](https://github.com/feelinglovelynow/get-form-entries)
* [@feelinglovelynow/get-relative-time](https://github.com/feelinglovelynow/get-relative-time)
* [@feelinglovelynow/global-style](https://github.com/feelinglovelynow/global-style)
* [@feelinglovelynow/jwt](https://github.com/feelinglovelynow/jwt)
* [@feelinglovelynow/loop-backwards](https://github.com/feelinglovelynow/loop-backwards)
* [@feelinglovelynow/slug](https://github.com/feelinglovelynow/slug)
* [@feelinglovelynow/svelte-loading-anchor](https://github.com/feelinglovelynow/svelte-loading-anchor)
* [@feelinglovelynow/svelte-modal](https://github.com/feelinglovelynow/svelte-modal)
* [@feelinglovelynow/svelte-turnstile](https://github.com/feelinglovelynow/svelte-turnstile)
* [@feelinglovelynow/toast](https://github.com/feelinglovelynow/toast)
