<script>
import zxcvbn from "zxcvbn";
import VuePassword from "./VuePassword.vue";

export default {
  name: "VuePasswordAuto",
  functional: true,
  components: { VuePassword },
  render(h, context) {
    const data = context.data;
    const inputs = Array.isArray(context.props.userInputs)
      ? context.props.userInputs
      : [];
    const strength = zxcvbn(data.props.value, inputs);

    return h(VuePassword, {
      props: {
        ...data.props,
        strength: strength ? strength.score : 0
      },
			on: context.listeners,
			scopedSlots: context.scopedSlots,
    });
  }
};
</script>
