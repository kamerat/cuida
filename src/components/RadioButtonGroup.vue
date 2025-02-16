<template>
	<span id="radioButton">
		<div
			:class="{'button-group': inline }"
		>
			<div
				v-for="(option, i) in options"
				:key="option.value"
				:class="{'radio-button__container--vertical': inline && i > 0}"
			>
				<label
					class="radio-button"
					:disabled="option.disabled || disabled"
					:for="option.value"
				>
					<input
						type="radio"
						:id="option.value"
						:value="option.value"
						v-model="selected"
						:disabled="option.disabled || disabled"
					>
					<label
						class="radio-button__content"
						:for="option.value"
					>
						{{ option.text }}
					</label>
				</label>
			</div>
		</div>
	</span>
</template>

<script>
export default {
	props: {
		/**
		 * A prop usada como v-model para monitorar a seleção do RadioButton
		*/
		value: {
			default: null,
			required: true,
		},
		/**
		 * O número de radio buttons a ser renderizado no grupo
		 */
		options: {
			type: Array,
			default: () => [],
			required: true,
		},
		/**
		 * Controla o status do grupo de radio buttons
		 */
		disabled: {
			type: Boolean,
			default: false,
			required: false,
		},
		/**
		 * Quando verdadeira, faz com que os radio buttons sejam renderizados um ao lado do outro
		 */
		inline: {
			type: Boolean,
			default: false,
			description: `When true, the radio buttons will be displayed in a row.`,
			required: false,
		},
	},

	data() {
		return {
			selected: this.value,
		};
	},

	watch: {
		selected(value) {
			this.$emit('input', value);
		},

		value: {
			handler(newValue) {
				this.selected = newValue;
			},
			immediate: true,
		},
	},
};
</script>
<style lang="scss">
@import '../assets/sass/app.scss';

#radioButton [type="radio"]:checked,
#radioButton [type="radio"]:not(:checked) {
	position: absolute;
	left: -9999px;
}

#radioButton [type="radio"]:checked + label,
#radioButton [type="radio"]:not(:checked) + label
{
	position: relative;
	padding: pl(7);
	cursor: pointer;
	line-height: 20px;
	display: inline-block;
	color: $n-600;
}

#radioButton [type="radio"]:checked + label:before,
#radioButton [type="radio"]:not(:checked) + label:before {
	content: '';
	position: absolute;
	left: 0;
	top: 0;
	width: 20px;
	height: 20px;
	border: 1px solid $n-800;
	border-radius: 100%;
	background: $n-0;
}

#radioButton [type="radio"]:checked + label:after,
#radioButton [type="radio"]:not(:checked) + label:after {
	content: '';
	width: 12px;
	height: 12px;
	background: $bn-600;
	position: absolute;
	top: 4px;
	left: 4px;
	border-radius: 100%;
	-webkit-transition: all 0.3s ease;
	transition: all 0.3s ease;
}

#radioButton [type="radio"]:not(:checked) + label:after {
	opacity: 0;
	-webkit-transform: scale(0);
	transform: scale(0);
}

#radioButton [type="radio"]:checked + label:after {
	opacity: 1;
	-webkit-transform: scale(1);
	transform: scale(1);
}

#radioButton .button-group {
	display: flex;
}

#radioButton .radio-button {
	border: 1px solid $n-50;
	padding: pYX(3, 4);
	border-radius: 0.5rem;
	cursor: pointer;
	display: inline-block;

	&__container--vertical {
		margin: ml(4);
	}

	&__content {
		margin: ma(0);
	}
}

#radioButton .radio-button:hover {
	background-color: $n-10;
	-webkit-transition: all 0.3s ease;
	transition: all 0.3s ease;
}

#radioButton .radio-button[disabled="disabled"] {
	background-color: $n-30;
	-webkit-transition: all 0.3s ease;
	transition: all 0.3s ease;
}

#radioButton .radio-button[disabled="disabled"]
	[type="radio"]:checked + label:before,
#radioButton .radio-button[disabled="disabled"]
	[type="radio"]:not(:checked) + label:before {
	background: transparent;
}
</style>
