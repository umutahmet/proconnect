<script>
	export let currentStep;
	export let totalSteps;
</script>

<div class="w-full bg-gray-200 rounded-full h-2.5 mb-4">
	<div
		class="bg-blue-600 h-2.5 rounded-full"
		style="width: {(currentStep / totalSteps) * 100}%"
	></div>
</div>

<style>
	/* Add any additional styles here */
</style>
