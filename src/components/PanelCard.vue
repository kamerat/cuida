<template>
	<div class="panel-card">
		<div class="panel-card__header">
			<div>
				<span class="panel-card__title">{{ title }}</span>
				<br>
				<span class="panel-card__subtitle">{{ subtitle }}</span>
			</div>
			<div class="ml-auto">
				<!-- @slot Slot usado para inserção de elemento à direita no header. -->
				<slot name="panel-actions" />
			</div>
		</div>
		<hr class="panel-card__divider">
		<div :class="contentClass">
			<!-- @slot Slot usado para inserção de conteúdo customizado. -->
			<slot />
		</div>
	</div>
</template>

<script>
export default {
	props: {
		/**
		 * Título do card.
		 */
		title: {
			type: String,
			default: 'Título',
			required: true,
		},
		/**
		 * Subtítulo do card.
		 */
		subtitle: {
			type: String,
			default: 'Subtítulo',
			required: true,
		},
		/**
		 * Remove o padding padrão do corpo do card.
		 */
		noContentPadding: {
			type: Boolean,
			default: false,
		},
	},

	computed: {
		contentClass() {
			if (this.noContentPadding) {
				return 'panel-card__content--no-pading';
			}
			return 'panel-card__content';
		},
	},
};
</script>

<style lang="scss" scoped>
@import '../assets/sass/app.scss';

.panel-card {
	background-color: $n-0;
	border-radius: $border-radius-extra-small;

	&__divider {
		margin: ma(0);
		color: $n-300;
	}

	&__header {
		padding: pa(4);
		display: flex;
		min-height: 78px;
	}

	&__content {
		padding: pa(4);
	}

	&__content--no-padding {
		padding: pa(4);
	}

	&__title {
		@include subheading-2;
		margin: mb(2);
		color: $n-900;
	}

	&__subtitle {
		@include subheading-3;
		color: $n-500;
	}
}
</style>
