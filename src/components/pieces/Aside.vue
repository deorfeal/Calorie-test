<script setup lang="ts"></script>

<template>
  <aside class="aside">
    <div class="aside__calories calories">
      <ul class="calories__list">
        <li class="calories__list-item" data-testid="calories-item-1">
          <div class="calories__list-text">Your target calories</div>
          <div class="calories__list-unit">
            <!--  -->
            <span> Kcal </span>
          </div>
        </li>
        <li class="calories__list-item" data-testid="calories-item-2">
          <div class="calories__list-text">Proteins</div>
          <div class="calories__list-unit">
            <!--  -->
            <span> g </span>
          </div>
        </li>
        <li class="calories__list-item" data-testid="calories-item-3">
          <div class="calories__list-text">Fats</div>
          <div class="calories__list-unit">
            <!--  -->
            <span> g </span>
          </div>
        </li>
        <li class="calories__list-item" data-testid="calories-item-4">
          <div class="calories__list-text">Carbs</div>
          <div class="calories__list-unit">
            <!--  -->
            <span> g </span>
          </div>
        </li>
      </ul>
    </div>
  </aside>
</template>

<style lang="scss">
.aside {
  display: flex;
  flex-direction: column;
  border-radius: 12px;
  border: 1px solid #4b515a;
  padding: 40px;
}

.calories {
  flex-grow: 1;
  margin-bottom: 30px;

  &:last-child {
    margin-bottom: unset;
  }
  &__list {
    display: flex;
    flex-direction: column;
    gap: 12px;
  }

  &__list-item {
    color: #fafaf9;
    font-size: 14px;
    line-height: 24px;
    letter-spacing: 0.3px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 30px;

    &:nth-child(1) {
      font-size: 16px;
      font-weight: 600;
      line-height: 24px;
      letter-spacing: 0.5px;
    }
  }

  &__list-text {
  }

  &__list-unit {
  }
}

@media (max-width: 550px) {
  .aside {
    padding: 30px;
  }

  .calories__list-item {
    font-size: 12px;
    line-height: 16px;

    &:nth-child(1) {
      font-size: 14px;
      line-height: 24px;
    }
  }

  .calories__list {
    margin-bottom: 25px;
  }
}
</style>
