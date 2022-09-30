<template>
  <div class="card text-start border-0 col-md-7 text-center">
    <div class="card-body p-0 gap-5">
      <img :src="completed" class="card-img-top m-5" alt="..." />
      <h3 class="card-title mb-3">THANK YOU!</h3>
      <p class="card-text mb-1">We've added your card details</p>
      <buttomn href="#" class="btn d-block mt-5 mb-2" @click="$emit('continue')">Continue</buttomn>
    </div>
  </div>
</template>
  
  <script>
import completeIcon from "../assets/images/icon-complete.svg";
export default {
  name: "Confirm",
  data() {
    return {
      completed: completeIcon,
    };
  },
};
</script>
  
  <style scoped>
.btn {
  padding: 0.7rem;
  background-color: var(--Very-dark-violet);
  color: white;
}
label {
  color: var(--Very-dark-violet);
  font-weight: 500;
}
img{
    width: 5rem;
}
</style>