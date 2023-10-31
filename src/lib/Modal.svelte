<script lang="ts">
  import type { ShowModal, HideModal } from '$lib'
  import { onMount, createEventDispatcher } from 'svelte'


  export let header: string = ''
  export let onHideModal: () => void = () => {}


  let setHideCss = false
  let isModalVisible = false
  const dispatch = createEventDispatcher()


  const showModal = (() => {
    document.body.classList.add('fln__modal-is-visible')
    document.body.style.overflow = 'hidden'
    document.addEventListener('keyup', onKeyup)
    setTimeout(() => {
      isModalVisible = true
    }, 150)
  }) satisfies ShowModal


  const hideModal = (() => {
    setHideCss = true
    document.body.style.overflow = 'auto'
    document.body.classList.remove('fln__modal-is-visible')

    setTimeout(() => {
      setHideCss = false
      isModalVisible = false
      onHideModal()
    }, 900)

    document.removeEventListener('keyup', onKeyup)
  }) satisfies HideModal


  onMount(() => {
    dispatch('functions', { showModal, hideModal })

    return () => {
      document.removeEventListener('keyup', onKeyup)
    }
  })


  function onKeyup (e: KeyboardEvent): void {
    if (e.key === 'Escape') hideModal()
  }
</script>


{ #if isModalVisible }
  <!-- svelte-ignore a11y-no-static-element-interactions -->
  <div on:click={ hideModal } on:keyup={ onKeyup } class="fln__modal-backdrop{ setHideCss ? ' hide': '' }">
    <div on:click|stopPropagation on:keyup={ onKeyup } class="fln__modal{ setHideCss ? ' hide': '' }">
      { #if header}
        <div class="fln__modal__header">
          <div class="fln__modal__header__text">{ header }</div>
          <button class="fln__modal__header__close" on:click={ hideModal } type="button">
            <svg role="img" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24"><title>Close Modal</title><path fill="currentColor" d="M18.3 5.71a.996.996 0 0 0-1.41 0L12 10.59L7.11 5.7A.996.996 0 1 0 5.7 7.11L10.59 12L5.7 16.89a.996.996 0 1 0 1.41 1.41L12 13.41l4.89 4.89a.996.996 0 1 0 1.41-1.41L13.41 12l4.89-4.89c.38-.38.38-1.02 0-1.4z"/></svg>
          </button>
        </div>
      { /if }
      <div class="fln__modal__body">
        <slot />
      </div>
    </div>
  </div>
{ /if }


<style lang="scss">
  @keyframes fln__modal-backdrop__blur {
    from {
      backdrop-filter: blur(0.01rem);
    }

    to {
      backdrop-filter: blur(0.72rem);
    }
  }

  .fln {
    &__modal-backdrop {
      position: fixed;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      width: 100%;
      height: 100%;
      opacity: 1;
      display: flex;
      justify-content: center;
      align-items: start;
      background-color: rgba(0, 0, 0, 0.54);
      backdrop-filter: blur(0.72rem);
      animation-name: fln__modal-backdrop__blur;
      animation-duration: 1.8s;
      padding: 2.7rem 0.9rem;
      overflow: auto;
      transition: all 0.9s;
      border: none;
      cursor: default;
      &.hide {
        opacity: 0;
      }
    }

    &__modal {
      width: 100%;
      max-width: 81rem;
      position: relative;
      border-radius: 1.8rem;
      animation-name: fln__fade-in-from-above;
      animation-duration: 0.9s;
      border: none;
      text-align: left;
      &.hide {
        animation-name: fln__fade-out-and-slide-up;
      }

      &__header {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 1.8rem 1.8rem 0 1.8rem;
        margin-bottom: -1.8rem;

        &__close {
          border: none;
          background-color: transparent;

          svg {
            height: 2.4rem;
            width: 2.4rem;
            cursor: pointer;
          }
        }
      }

      &__body {
        margin: 0;
        padding: 1.8rem;
      }
    }
  }
</style>
