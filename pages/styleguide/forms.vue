<template>
  <StyleguideLayout :component-name="title">
    <form>
      <div>
        <label>Label</label>
        <input type="text" value="Text input">
      </div>
      <div class="sml-push-y2">
        <label>Label</label>
        <input type="text" placeholder="Placeholder text">
      </div>
      <div class="sml-push-y2">
        <label>Label</label>
        <textarea>Textarea</textarea>
      </div>
      <div class="row">
        <div class="sml-c12 med-c6 sml-push-y2">
          <label>Label</label>
          <input type="text" placeholder="Placeholder text">
        </div> <!-- .c -->
        <div class="sml-c12 med-c6 sml-push-y2">
          <label>Label</label>
          <input type="text" placeholder="Placeholder text">
        </div> <!-- .c -->
      </div> <!-- .row -->
      <div class="sml-push-y2">
        <label>Label</label>
        <input type="text" value="Error Field" class="error">
      </div>
      <div class="sml-push-y2">
        <label>Label</label>
        <textarea class="error">Textarea</textarea>
      </div>
      <div class="sml-push-y2">
        <label>Dropdown menu</label>
        <div class="select">
          <select>
            <option>Option 1</option>
            <option>Option 2</option>
            <option>Option 3</option>
            <option>Option 4</option>
            <option>Option 5</option>
          </select>
        </div> <!-- .select -->
      </div>
      <div class="checkbox sml-push-y2">
        <input id="checkbox-1" type="checkbox">
        <label for="checkbox-1">Checkbox label</label>
      </div>
      <div class="radio sml-push-y2">
        <input id="radio-1" type="radio" name="radio-example">
        <label for="radio-1">Radio label 1</label>
      </div>
      <div class="radio sml-push-y2">
        <input id="radio-2" type="radio" name="radio-example">
        <label for="radio-2">Radio label 2</label>
      </div>
      <div class="sml-push-y2 flex-grid sml-flex-row">
        <div class="faux-btn">
          <input id="radio-button-yes" type="radio" name="radio-button">
          <label for="radio-button-yes">Radio button: yes</label>
        </div> <!-- .faux-btn -->
        <div class="faux-btn">
          <input id="radio-button-no" type="radio" name="radio-button">
          <label for="radio-button-no">Radio button: no</label>
        </div> <!-- .faux-btn -->
      </div>
      <div class="sml-push-y2">
        <button type="submit" class="btn block">Submit</button>
      </div> <!-- div.submit -->
    </form>

    <form class="sml-push-y2 sml-pad-y2 with-border-top">
      <label>Form field with inline button</label>
      <div class="row">
        <div class="sml-c8">
          <input type="text">
        </div> <!-- .c -->
        <div class="sml-c4">
          <button type="submit" class="btn btn-block">Submit</button>
        </div> <!-- .c -->
      </div> <!-- .row -->
    </form>
  </StyleguideLayout>
</template>

<script>
import StyleguideLayout from '~/components/StyleguideLayout'

export default {
  components: {
    StyleguideLayout
  },

  computed: {
    title() { return 'Forms' }
  }
}
</script>
