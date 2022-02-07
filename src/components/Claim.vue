<template>
  <div class="claimWrapper">
    <h1 class="claim">SPACER</h1>
    <p class="subclaim">
      Begin your journey through our amazing galaxy,
      and discover places you never even heard of.
    </p>
    <p class="subclaim">
      Type anything space-related to start.
    </p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style scoped lang="scss">
.claimWrapper{
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: #ffffff;
  width: 100%;
  margin: 0 auto;
  @media (max-width: 768px) {
    max-width: 600px;
  }
  .claim{
    margin: 0;
    font-size: 80px;
    @media (max-width: 768px) {
      font-size: 50px;
    }
  }
  .subclaim{
    margin: 20px 0 0 0;
    font-weight: 400;
    font-size: 20px;
    @media (max-width: 768px) {
      font-size: 18px;
    }
  }
}
</style>
