<template>
  <base-dialog
    :value="value"
    @input="updateValue(arguments[0])"
    :child="this"
    @ok="create"

    @showed="showed">
      <v-layout row wrap>
        <v-flex xs12>
          <v-text-field
            label="Username"
            placeholder="Username"
            v-model="username"
            ref="focus"
          ></v-text-field>
        </v-flex>
        <v-flex xs12>
          <v-text-field
            label="Password"
            placeholder="Password"
            v-model="password"
          ></v-text-field>
        </v-flex>
          <v-flex xs12>
          <v-text-field
            label="DisplayName"
            placeholder="DisplayName"
            v-model="display_name"
          ></v-text-field>
        </v-flex>
      </v-layout>
  </base-dialog>
</template>

<script>
import baseDialog from '@/components/base_dialog';

export default {
  components: {
    baseDialog,
  },
  props: {
    value: false,
  },
  data() {
    return {
      username: '',
      display_name: '',
      password: '',
    };
  },
  methods: {
    updateValue(value) {
      this.$emit('input', value);
    },
    create() {
      this.$store.dispatch('create_user', {
        username: this.username,
        display_name: this.display_name,
        password: this.password,
      })
        .catch(() => {
        });
      this.updateValue(false);
    },
    showed() {
      this.username = '';
      this.password = '';
      this.display_name = '';
    },
  },
};
</script>
