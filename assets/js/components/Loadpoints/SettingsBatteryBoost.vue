<template>
	<div>
		<h6>
			{{ $t("main.loadpointSettings.batteryUsage") }}
		</h6>

		<div class="mb-3 row" data-testid="battery-boost">
			<label :for="formId('batteryBoost')" class="col-sm-4 col-form-label pt-0 pt-sm-2">
				{{ $t("main.loadpointSettings.batteryBoost.label") }}&nbsp;🧪
			</label>
			<div class="col-sm-8 pe-0">
				<div class="form-check form-switch my-1">
					<input
						:id="formId('batteryBoost')"
						v-model="selectedEnabled"
						class="form-check-input"
						type="checkbox"
						role="switch"
						:disabled="disabled"
						data-testid="battery-boost-checkbox"
						@change="handleEnabledChange"
					/>
					<label :for="formId('batteryBoost')" class="form-check-label">
						<div>
							{{ $t("main.loadpointSettings.batteryBoost.description") }}
						</div>
						<span v-if="selectedEnabled && !disabled" class="d-block text-primary">
							{{ $t("main.loadpointSettings.batteryBoost.once") }}
						</span>
						<small v-if="disabled" class="d-block">
							{{ $t("main.loadpointSettings.batteryBoost.mode") }}
						</small>
					</label>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import formatter from "../../mixins/formatter.js";

export default {
	mixins: [formatter],
	props: {
		formId: Function,
		mode: String,
		batteryBoost: Boolean,
	},
	emits: ["batteryboost-updated"],
	data() {
		return {
			selectedEnabled: this.batteryBoost,
		};
	},
	computed: {
		disabled() {
			return ["off", "now"].includes(this.mode);
		},
	},
	watch: {
		batteryBoost(newVal) {
			this.selectedEnabled = newVal;
		},
	},
	methods: {
		handleEnabledChange() {
			this.$emit("batteryboost-updated", this.selectedEnabled);
		},
	},
};
</script>
