<script>
	export let currentStep = 1;
	export let totalSteps = 1;

	$: progress = (currentStep / totalSteps) * 100;
</script>

<div class="flex items-center gap-4">
	<div class="w-full bg-neutral-200 rounded-full h-1">
		<div
			class="bg-neutral-800 h-1 rounded-full transition-all duration-300 ease-in-out"
			style="width: {progress}%"
		></div>
	</div>

	<div class="text-xs text-neutral-600 font-semibold text-right flex-shrink-0">
		{currentStep} / {totalSteps}
	</div>
</div>
