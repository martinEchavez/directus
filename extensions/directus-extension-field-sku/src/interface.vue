<template>
	<div class="generate-sku">
		<v-input v-bind="value" disabled>
			<template #prepend>
				<v-icon name="perm_identity" />
			</template>
		</v-input>
		<v-button @click="generateSKU" icon><v-icon name="refresh" /></v-button>
	</div>
</template>
  
<script>
import { useApi, useStores } from "@directus/extensions-sdk";

export default {
	props: {
		value: {
			type: String,
			default: false,
		},
	},
	setup() {
		const api = useApi();

		const { useCollectionsStore, useFieldsStore } = useStores();
		const collectionsStore = useCollectionsStore();
		const fieldsStore = useFieldsStore();
	},
	data: function () {
		return {
			collections: null,
			data: [],
		};
	},

	emits: ["input"],

	mounted: function () {

		if (!this.value) {
			let init = this.generateSKU();
			this.$emit("input", init);
		}
	},

	methods: {
		/**
		 * Get a new generate-sku for the value
		 */
		async generateSKU() {
			let min = Math.ceil(100000);
			let max = Math.floor(999999);
			let sku = Math.floor(Math.random() * (max - min + 1)) + min;
			//let sku = "121232"

			//let { data: { data } } = await this.api.get("/items/items?filter[sku]=" + sku + "&limit=1");
			let data = "212521"
			console.log(data)
			
			if (data.length) {
				this.generateSKU();
				return
			}
		
			console.log("sku -------",sku)
			this.$emit("input", sku);
			return sku;
		},
	},
	inject: ["api"],
};
</script>
  
<style scoped>
.generate-sku {
	display: flex;
	justify-content: space-between;
	gap: 15px;
}
</style>
  