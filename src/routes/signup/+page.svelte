<script>
	import { onMount } from 'svelte';
	import ProgressBar from '$lib/components/progress-bar.svelte';

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

<div class="flex h-screen pt-28">
	<div class="w-1/2 overflow-y-auto p-8">
		<h1 class="text-3xl font-bold mb-6">Recruiter Registration</h1>
		<ProgressBar {currentStep} {totalSteps} />

		<form on:submit|preventDefault={handleSubmit} class="space-y-6 mt-8">
			{#if currentStep === 1}
				<section>
					<h2 class="text-2xl font-semibold mb-4">Identification</h2>

					<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
						<div>
							<label for="name" class="block mb-2">Name</label>
							<input
								type="text"
								id="name"
								bind:value={formData.name}
								required
								class="w-full p-2 border rounded"
							/>
						</div>

						<div>
							<label for="agencyName" class="block mb-2">Agency Name</label>
							<input
								type="text"
								id="agencyName"
								bind:value={formData.agencyName}
								required
								class="w-full p-2 border rounded"
							/>
						</div>

						<div>
							<label class="block mb-2">
								<input type="checkbox" bind:checked={formData.isIndependent} />
								Are you an Independent business owner?
							</label>
						</div>

						<div>
							<label for="dateIncorporated" class="block mb-2">Date Incorporated</label>
							<input
								type="date"
								id="dateIncorporated"
								bind:value={formData.dateIncorporated}
								class="w-full p-2 border rounded"
							/>
						</div>
					</div>
				</section>
			{:else if currentStep === 2}
				<section>
					<h2 class="text-2xl font-semibold mb-4">Online Presence</h2>

					<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
						<div>
							<label for="linkedInProfile" class="block mb-2">LinkedIn Profile</label>
							<input
								type="url"
								id="linkedInProfile"
								bind:value={formData.linkedInProfile}
								class="w-full p-2 border rounded"
							/>
						</div>

						<div>
							<label for="sourcr" class="block mb-2">Sourcr Profile</label>
							<input
								type="url"
								id="sourcr"
								bind:value={formData.sourcr}
								class="w-full p-2 border rounded"
							/>
						</div>

						<div>
							<label for="website" class="block mb-2">Website</label>
							<input
								type="url"
								id="website"
								bind:value={formData.website}
								class="w-full p-2 border rounded"
							/>
						</div>

						<div>
							<label for="otherSocialMedia" class="block mb-2">Other Social Media</label>
							<input
								type="text"
								id="otherSocialMedia"
								bind:value={formData.otherSocialMedia}
								class="w-full p-2 border rounded"
							/>
						</div>
					</div>
				</section>
			{:else if currentStep === 3}
				<section>
					<h2 class="text-2xl font-semibold mb-4">Location & Bio</h2>

					<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
						<div>
							<label for="residentialLocation" class="block mb-2">Residential Location</label>
							<input
								type="text"
								id="residentialLocation"
								bind:value={formData.residentialLocation}
								required
								class="w-full p-2 border rounded"
							/>
						</div>

						<div>
							<label for="officeLocation" class="block mb-2">Office Location (optional)</label>
							<input
								type="text"
								id="officeLocation"
								bind:value={formData.officeLocation}
								class="w-full p-2 border rounded"
							/>
						</div>
					</div>

					<div class="mt-4">
						<label for="bioSummary" class="block mb-2"
							>Bio Summary (Unique Selling Factor statement)</label
						>
						<textarea
							id="bioSummary"
							bind:value={formData.bioSummary}
							rows="4"
							class="w-full p-2 border rounded"
						></textarea>
					</div>

					<div class="mt-4">
						<label for="video" class="block mb-2">Video Upload</label>
						<input
							type="file"
							id="video"
							accept="video/*"
							on:change={handleFileChange}
							class="w-full p-2 border rounded"
						/>
					</div>
				</section>
			{:else if currentStep === 4}
				<section>
					<h2 class="text-2xl font-semibold mb-4">Business Details</h2>

					<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
						<div>
							<label class="block mb-2">
								<input type="checkbox" bind:checked={formData.adminSupport} />
								Do you have admin support?
							</label>
						</div>

						<div>
							<label class="block mb-2">
								<input type="checkbox" bind:checked={formData.inHouseTempTeam} />
								Do you have an in-house temp team?
							</label>
						</div>
					</div>

					<div class="mt-4">
						<label for="teamSetup" class="block mb-2">Team Setup</label>
						<textarea
							id="teamSetup"
							bind:value={formData.teamSetup}
							rows="3"
							class="w-full p-2 border rounded"
						></textarea>
					</div>

					<div class="mt-4">
						<label for="otherOfferings" class="block mb-2">Other Offerings</label>
						<textarea
							id="otherOfferings"
							bind:value={formData.otherOfferings}
							rows="3"
							class="w-full p-2 border rounded"
						></textarea>
					</div>

					<div class="mt-4">
						<label for="policies" class="block mb-2">Policies & Terms</label>
						<textarea
							id="policies"
							bind:value={formData.policies}
							rows="3"
							class="w-full p-2 border rounded"
						></textarea>
					</div>

					<div class="mt-4">
						<label for="insurances" class="block mb-2">Insurances</label>
						<textarea
							id="insurances"
							bind:value={formData.insurances}
							rows="3"
							class="w-full p-2 border rounded"
						></textarea>
					</div>
				</section>
			{:else if currentStep === 5}
				<section>
					<h2 class="text-2xl font-semibold mb-4">Specialization</h2>

					<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
						<div>
							<label for="industrySpecialization" class="block mb-2">Industry Specialization</label>
							<input
								type="text"
								id="industrySpecialization"
								bind:value={formData.industrySpecialization}
								required
								class="w-full p-2 border rounded"
							/>
						</div>

						<div>
							<label for="dateStartedIndustry" class="block mb-2">Date Started in Industry</label>
							<input
								type="date"
								id="dateStartedIndustry"
								bind:value={formData.dateStartedIndustry}
								required
								class="w-full p-2 border rounded"
							/>
						</div>

						<div>
							<label for="totalYearsExperience" class="block mb-2">Total Years of Experience</label>
							<input
								type="number"
								id="totalYearsExperience"
								bind:value={formData.totalYearsExperience}
								required
								class="w-full p-2 border rounded"
							/>
						</div>

						<div>
							<label for="dateStartedRecruiting" class="block mb-2"
								>Date Started Recruiting (end to end)</label
							>
							<input
								type="date"
								id="dateStartedRecruiting"
								bind:value={formData.dateStartedRecruiting}
								required
								class="w-full p-2 border rounded"
							/>
						</div>

						<div>
							<label for="recruitmentReach" class="block mb-2">Location Scope of Recruitment</label>
							<input
								type="text"
								id="recruitmentReach"
								bind:value={formData.recruitmentReach}
								required
								class="w-full p-2 border rounded"
							/>
						</div>

						<div>
							<label for="dateStartedInLocation" class="block mb-2"
								>Date Started Recruiting in Location</label
							>
							<input
								type="date"
								id="dateStartedInLocation"
								bind:value={formData.dateStartedInLocation}
								required
								class="w-full p-2 border rounded"
							/>
						</div>

						<div>
							<label for="salaryLevelRecruit" class="block mb-2"
								>Salary Level Recruited (for client searching)</label
							>
							<input
								type="text"
								id="salaryLevelRecruit"
								bind:value={formData.salaryLevelRecruit}
								required
								class="w-full p-2 border rounded"
							/>
						</div>
					</div>
				</section>
			{:else if currentStep === 6}
				<section>
					<h2 class="text-2xl font-semibold mb-4">Fees & Terms</h2>

					<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
						<div>
							<label for="feesAndMargins" class="block mb-2">Fees & Margins</label>
							<textarea
								id="feesAndMargins"
								bind:value={formData.feesAndMargins}
								rows="3"
								class="w-full p-2 border rounded"
							></textarea>
						</div>

						<div>
							<label for="feeStructure" class="block mb-2"
								>Fee Structure (min/max for salary bands)</label
							>
							<textarea
								id="feeStructure"
								bind:value={formData.feeStructure}
								rows="3"
								class="w-full p-2 border rounded"
							></textarea>
						</div>

						<div>
							<label for="marginRange" class="block mb-2"
								>Margin Range and Structure for Temps</label
							>
							<textarea
								id="marginRange"
								bind:value={formData.marginRange}
								rows="3"
								class="w-full p-2 border rounded"
							></textarea>
						</div>
					</div>
				</section>
				<section>
					<h2 class="text-2xl font-semibold mb-4">Terms Agreement</h2>

					<div class="space-y-2">
						<label class="flex items-center">
							<input type="checkbox" bind:checked={formData.agreesToTerms} required />
							<span class="ml-2">I agree to be the one leading the process</span>
						</label>

						<label class="flex items-center">
							<input type="checkbox" required />
							<span class="ml-2"
								>I will virtually / in person meet with candidates prior to representing</span
							>
						</label>

						<label class="flex items-center">
							<input type="checkbox" required />
							<span class="ml-2"
								>I will ask standard interview questions prior to representing the candidate</span
							>
						</label>

						<label class="flex items-center">
							<input type="checkbox" required />
							<span class="ml-2"
								>I understand that negative feedback will result in a permanent ban for breaking the
								rules</span
							>
						</label>

						<label class="flex items-center">
							<input type="checkbox" required />
							<span class="ml-2"
								>I understand that positive feedback will promote my services in searches</span
							>
						</label>

						<label class="flex items-center">
							<input type="checkbox" required />
							<span class="ml-2">I agree to adhere to RCSA guidelines and code of conduct</span>
						</label>
					</div>
				</section>
			{/if}

			<div class="flex justify-between mt-8">
				{#if currentStep > 1}
					<button
						type="button"
						on:click={prevStep}
						class="bg-neutral-200 text-black px-6 py-2 rounded-lg hover:bg-neutral-300"
					>
						Previous
					</button>
				{:else}
					<div></div>
				{/if}

				{#if currentStep < totalSteps}
					<button
						type="button"
						on:click={nextStep}
						class="bg-lime-500 text-white px-6 py-2 rounded-lg hover:bg-lime-600"
					>
						Next
					</button>
				{:else}
					<button
						type="submit"
						class="bg-black text-white px-6 py-2 rounded-lg hover:bg-neutral-800"
					>
						Submit Registration
					</button>
				{/if}
			</div>
		</form>
	</div>

	<div
		class="w-1/2 bg-cover bg-center"
		style="background-image: url('https://images.unsplash.com/photo-1598962134959-27a16982a4db?q=80&w=3566&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D');"
	>
		<!-- You can add some overlay text or logo here if needed -->
	</div>
</div>

<style>
	/* Add any additional styles here */
</style>
