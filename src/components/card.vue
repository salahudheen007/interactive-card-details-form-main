<template>
  <div class="card text-start border-0">
    <form action="" @submit="$emit('confirmed')">
      <div class="card-body p-0 gap-5">
      <div>
        <label for="name" class="mt-3 mb-2 form-label">CARDHOLDER NAME</label>
      <input
        type="text"
        name="name"
        id="name"
        placeholder="e.g Jane Appleseed"
        class="form-control d-block py-2"
        @change="$emit('updateCard', cardDetails1)"
        v-model="cardDetails1.name"
        required
      />
      <div class="invalid-feedback">Please fill out this field.</div>
      </div>
      <label for="cardnumber" class="mt-3 mb-2">CARD NUMBER</label>
      <input
        type="number"
        id="cardnumber"
        class="form-control py-2 d-block"
        placeholder="e.g 0000 0000 0000 0000"
        @change="$emit('updateCard', cardDetails1)"
        v-model="cardDetails1.cardNumber"
        ref="cardNum"
        required
      />
      <div class="row">
        <div class="div col">
          <label for="EXPDAR" class="mt-3 mb-2">EXP. DATE(MM/YY)</label>
          <div class="div row">
            <div class="col">
              <input
                type="NUMBER"
                name=""
                id="month"
                placeholder="MM"
                class="form-control py-2"
                @change="$emit('updateCard', cardDetails1)"
                v-model="cardDetails1.expdatMM"
                required
              />
            </div>
            <div class="col">
              <input
                type="NUMBER"
                name=""
                id="year"
                placeholder="YY"
                class="form-control py-2"
                @change="$emit('updateCard', cardDetails1)"
                v-model="cardDetails1.expdatYY"
                required
              />
            </div>
          </div>
        </div>
        <div class="div col">
          <Label for="CVC" class="mt-3 mb-2">CVC</Label>
          <input
            type="NUMBER"
            name="CVC"
            id="CVC"
            placeholder="e.g 123"
            class="form-control py-2"
            v-model="cardDetails1.cvv"
            @change="$emit('updateCard', cardDetails1)"
            required
          />
        </div>
      </div>
      <input type="submit"  class="btn d-block mt-4 mb-2" value="Confirm">
    </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "Card",
  data() {
    return {
      cardDetails1: {
        cvv: "",
        name: "",
        cardNumber: "",
        expdatMM: "",
        expdatYY: "",
      },
    };
  },
  methods: {
    addSpace() {
      if (this.$refs.cardNum.value.length > 0) {
        if (this.$refs.cardNum.value.length % 4 == 0) {
          this.$refs.cardNum.value+= " ";
        }
      }
    },
  },
};
</script>

<style scoped>
.btn {
  padding-left: 40%;
  background-color: var(--Very-dark-violet);
  color: white;
  padding-right: 40%;
}
label {
  color: var(--Very-dark-violet);
  font-weight: 500;
}
.card {
  max-width: 27rem;
}
</style>