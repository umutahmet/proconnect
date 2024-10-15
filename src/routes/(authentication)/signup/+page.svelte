<script>
	import { onMount } from 'svelte';
	import ProgressBar from '$lib/components/progress-bar.svelte';
	import SignupForm from '$lib/components/auth/signup-form.svelte';

	let currentStep = 1;
	const totalSteps = 6;

	let formData = {
		name: '',
		agencyName: '',
		isIndependent: false,
		dateIncorporated: '',
		linkedInProfile: '',
		sourcr: '',
		website: '',
		otherSocialMedia: '',
		residentialLocation: '',
		officeLocation: '',
		bioSummary: '',
		video: null,
		adminSupport: false,
		inHouseTempTeam: false,
		teamSetup: '',
		otherOfferings: '',
		policies: '',
		insurances: '',
		industrySpecialization: '',
		dateStartedIndustry: '',
		totalYearsExperience: '',
		dateStartedRecruiting: '',
		recruitmentReach: '',
		dateStartedInLocation: '',
		salaryLevelRecruit: '',
		feesAndMargins: '',
		feeStructure: '',
		marginRange: '',
		agreesToTerms: false
	};

	let videoFile;

	const handleSubmit = () => {
		if (!formData.agreesToTerms) {
			return alert('You must agree to the terms and conditions.');
		}

		console.log('Form submitted:', formData);
	};

	const handleFileChange = (event) => {
		const file = event.target.files[0];
		if (file) {
			formData.video = file;
		}
	};

	const nextStep = () => {
		if (currentStep < totalSteps) {
			currentStep++;
		}
	};

	const prevStep = () => {
		if (currentStep > 1) {
			currentStep--;
		}
	};

	onMount(() => {
		// Any initialization code can go here
	});
</script>

<div class="lg:flex h-screen">
	<div class="lg:w-1/2 overflow-y-auto p-8">
		<div class="flex flex-col justify-center items-center lg:max-w-xl lg:mx-auto w-full h-full">
			<div class="w-full">
				<ProgressBar {currentStep} {totalSteps} />
				<SignupForm {handleSubmit} {handleFileChange} {currentStep} {formData} />

				<div class="flex justify-end gap-2 mt-8">
					<button
						type="button"
						on:click={prevStep}
						disabled={currentStep === 1}
						class="bg-neutral-200 text-black font-semibold px-6 py-2 hover:bg-neutral-300 disabled:text-neutral-400 disabled:hover:bg-neutral-200"
					>
						Previous
					</button>

					{#if currentStep < totalSteps}
						<button
							type="button"
							on:click={nextStep}
							class="bg-neutral-800 font-semibold text-white px-6 py-2 hover:bg-neutral-700"
						>
							Next
						</button>
					{:else}
						<button
							type="submit"
							class="bg-black font-semibold text-white px-6 py-2 hover:bg-neutral-800"
						>
							Submit Registration
						</button>
					{/if}
				</div>
			</div>
		</div>
	</div>

	<div
		class="hidden lg:block lg:w-1/2 bg-cover bg-center relative"
		style="background-image: url('/assets/images/woman-2.jpg');"
	>
		<div class="absolute inset-0 bg-black bg-opacity-20"></div>
		<div class="absolute inset-0 flex items-center justify-center">
			<div class="p-24 text-center">
				<p class="text-white text-4xl font-exo mb-4">
					"This platform has revolutionized our recruitment process. It's empowering and efficient!"
				</p>
				<p class="text-white font-light">Sarah Johnson, HR Director at TechCorp</p>
			</div>
		</div>
	</div>
</div>

<style>
	/* Add any additional styles here */
</style>
