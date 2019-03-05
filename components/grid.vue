<style lang="scss" scoped>
.grid-example {
  overflow: hidden;
}
@for $i from 1 through 12 {
  .grid-example .sml-c#{$i},
  .grid-example .med-c#{$i},
  .grid-example .lrg-c#{$i} {
    background: $grey-light-color;
    overflow: hidden;
  }
}
.grid-example p {
  margin-top:    16px;
  margin-bottom: 16px;
  background: $brand-color;
  color: $white;
  line-height: 2;
  text-align: center;
}
.grid-example p {
  font-size: 14px;
}
</style>

<template>
  <div>
    <div class="grid-example">
      <h2>Default Grid Columns</h2>
      <div class="row sml-push-y1">
        <div class="med-hide lrg-c2"><p>med-hide lrg-c2</p></div>
        <div class="sml-c12 lrg-c8"><p>sml-c12 lrg-c8</p></div>
        <div class="med-hide lrg-c2"><p>med-hide lrg-c2</p></div>
      </div> <!-- .row -->

      <h2 class="sml-push-y4">Centered Grid Column</h2>
      <div class="row sml-push-y1">
        <div class="sml-c12 lrg-c8 grid-center">
          <p>sml-c12 lrg-c8 grid-center</p>
        </div> <!-- .c -->
      </div> <!-- .row -->

      <h2 class="sml-push-y4">
        Large: 2/3 and 1/3, Medium: 1/2 and 1/2, Small: full-width (optional sticky footer)
      </h2>
      <div class="row sml-push-y1">
        <div class="sml-c12 med-c6 lrg-c8"><p>sml-c12 med-c6 lrg-c8</p></div>
        <div class="sml-c12 med-c6 lrg-c4"><p>sml-c12 med-c6 lrg-c4</p></div>
      </div> <!-- .row -->

      <h2 class="sml-push-y4">
        Reponsive row overrides with sml-, med-, and lrg- classes
      </h2>
      <div class="row sml-push-y1">
        <div class="sml-c6 lrg-c2"><p>sml-c6 lrg-c2</p></div>
        <div class="sml-c6 lrg-c10"><p>sml-c6 lrg-c10</p></div>
      </div> <!-- .row -->
      <div class="row sml-push-y1">
        <div class="sml-c6 lrg-c4"><p>sml-c6 lrg-c4</p></div>
        <div class="sml-c6 lrg-c4"><p>sml-c6 lrg-c4</p></div>
        <div class="sml-c12 lrg-c4"><p>sml-c12 lrg-c4</p></div>
      </div> <!-- .row -->

      <div class="row sml-push-y1">
        <div class="sml-c6 med-c4 lrg-c2"><p>sml-c6 med-c4 lrg-c2</p></div>
        <div class="sml-c6 med-c4 lrg-c2"><p>sml-c6 med-c4 lrg-c2</p></div>
        <div class="sml-c6 med-c4 lrg-c2"><p>sml-c6 med-c4 lrg-c2</p></div>
        <div class="sml-c6 med-c4 lrg-c2"><p>sml-c6 med-c4 lrg-c2</p></div>
        <div class="sml-c6 med-c4 lrg-c2"><p>sml-c6 med-c4 lrg-c2</p></div>
        <div class="sml-c6 med-c4 lrg-c2"><p>sml-c6 med-c4 lrg-c2</p></div>
      </div> <!-- .row -->

      <h2 class="sml-push-y4">Nesting Columns in Columns. Make sure to use rows!</h2>
      <div class="row sml-push-y1">
        <div class="sml-c12 lrg-c6">
          <div class="row">
            <div class="sml-c6"><p>sml-c6</p></div>
            <div class="sml-c6"><p>sml-c6</p></div>
          </div> <!-- .row -->
          <div class="row">
            <div class="sml-c6"><p>sml-c6</p></div>
            <div class="sml-c6"><p>sml-c6</p></div>
          </div> <!-- .row -->
        </div> <!-- .c -->
      </div> <!-- .row -->
    </div> <!-- .grid-example -->
  </div>
</template>
