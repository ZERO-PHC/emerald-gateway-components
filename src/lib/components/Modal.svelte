<script>
        import { createEventDispatcher } from 'svelte';
        import { modal, tokens } from "../stores"
        import VerticalSpace from "../components/VerticalSpace.svelte"
        import Icon from "@iconify/svelte"

        export let isOpenModal;
        let isHovered;

        const dispatch = createEventDispatcher();


        function closeModal() {
        isOpenModal = false;
        isHovered = false;
        dispatch('closeModal', { isOpenModal });
    }

    const handleClick = () => isOpenModal = false

</script>

<div
  id="background"
  style="--display: {isOpenModal ? 'block' : 'none'}"
  on:click={closeModal}
/>
<main id="modal" style="--display: {isOpenModal ? 'block' : 'none'};">
  <header>
    <div>
      <span>MODAL TITLE</span>
    </div>
    <div>
      <!-- svelte-ignore missing-declaration -->
      <div
        on:click={handleClick}
        on:pointerenter={() => (isHovered = !isHovered)}
        on:pointerleave={() => (isHovered = !isHovered)}
      >
        <Icon
          icon="ant-design:close-circle-outlined"
          height={"1.4rem"}
          color={isHovered ? "var(--primary)" : "lightgrey"}
        />
      </div>
    </div>
  </header>
  <section>
    <div style="width:80%">
      <h6>Input 1</h6>
      <input placeholder="Input 1" />
    </div>
    <VerticalSpace value="1rem" />
    <div style="width:80%">
      <h6>Input 2</h6>
      <input placeholder="Input 2" />
    </div>
  </section>
  <footer >
    <div style="cursor: pointer;" on:click={handleClick}>
    ACTION 2

    </div>
  </footer>
</main>

<style>
  header {
    display: flex;
    flex-direction: row;
    height: 12%;
    width: 100%;
    justify-content: space-between;
    align-items: center;
    padding-right: 2rem;
    padding-left: 2rem;

    border-bottom: 2px solid var(--form-element-border-color);
  }

  section {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    height: 73%;
    width: 100%;
  }

  footer {
    color: var(--primary);
    display: flex;
    justify-content: flex-end;
    align-items: center;
    padding-right: 2rem;
    height: 15%;
    width: 100%;
    border-top: 2px solid var(--form-element-border-color);
  }

  #background {
    display: var(--display);
    position: fixed;
    z-index: 1;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.7);
  }

  #modal {
    display: var(--display);
    position: fixed;
    z-index: 2;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: #141e26;
    filter: drop-shadow(0 0 20px #333);
    height: 48%;
    width: 42%;
    border-radius: 20px;
    border: 2px solid var(--form-element-border-color);
  }
</style>
