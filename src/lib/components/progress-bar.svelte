<script>
	export let currentStep = 1;
	export let totalSteps = 1;

	$: progress = (currentStep / totalSteps) * 100;
</script>

<div class="w-full bg-gray-200 rounded-full h-2.5 mb-4">
	<div
		class="bg-lime-500 h-2.5 rounded-full transition-all duration-300 ease-in-out"
		style="width: {progress}%"
	></div>
</div>

<div class="text-sm text-gray-600 text-center">
	Step {currentStep} of {totalSteps}
</div>
