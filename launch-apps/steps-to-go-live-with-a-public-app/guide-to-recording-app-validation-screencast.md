# Guide to recording app validation screencast

The following guide will help you create a clear showcase of your app's functionalities. A well-structured video tour of your app will ensure that it is ready to be used by real Ecwid customers and passes verification with ease.

### Technical Specifications for Your Video

* Resolution: A minimum resolution of Full HD (1920x1080) is required for optimal clarity.
* Video Quality: Maintain high bitrate, avoiding pixelation.
* Audio: Utilize a high-quality microphone to ensure clear audio and minimize background noise.
  * Pro Tip: A smartphone's voice recorder can serve as an effective alternative if a dedicated microphone is unavailable; the audio can be synced with your video later in the editor.
* Format: Please use the MP4 format.
* Length: Aim to keep the video under 15 minutes. While thoroughness is important, please edit out or speed up any pauses or extended loading times.
* Pacing: Speak clearly and at a moderate pace. Move your mouse deliberately to allow us to follow your actions. Highlighting clicks and cursor movements can be very helpful.
* Language: The app interface and speech on the screen recording must be in English. Subtitles are also available.&#x20;
  * Note: if the service to which your app provides access, or the app itself, is available in foreign languages, you should demonstrate switching the interface language in the recording.
* Submission: Share your video via a direct download link from a reputable cloud service (e.g., Google Drive, Dropbox). The link must be publicly accessible, free to download, and valid for a minimum of 30 days. Include this link in your App Readiness Form.

### Screencast Content: Your Script

#### Step 1: Introduction (approximately 30 seconds)

* Begin with a clean desktop displaying your Ecwid test store.
* Introduce yourself and your app: "Hello, I'm \[your name] from \[your company]. This is the validation video for our new application, \[your app's name]."
* Briefly explain your app's purpose: "Our app assists Ecwid merchants in addressing \[the problem] by enabling them to \[main function/value]."

#### Step 2: Installation & Onboarding (approximately 1 minute)

* Demonstrate the installation process using your private "-dev" app link.
* When the OAuth permissions screen appears, provide a concise explanation for each requested permission.
* Showcase the initial merchant experience post-installation, including any welcome messages, setup wizards, or configuration pages. Guide us through these initial steps.

#### Step 3: Core Functionality Showcase (approximately 3-8 minutes)

* This section is critical for demonstrating your app's operational capabilities.
* Present each main feature from your App Market description, one by one.
* The "Show and Tell" Method:
  * State your action: "First, I will demonstrate our bulk price editor."
  * Perform the action: Utilize your app's interface to modify prices for several products.
  * Verify the action (critically important!): Navigate to the Ecwid Control Panel (e.g., Catalog > Products) and confirm that the prices have been successfully updated. This validates your API's functionality.
* Third-party integrations (if applicable):
  * Illustrate how your app connects to the external service.
  * Demonstrate data sync between Ecwid and the app/3rd party service by changing some data on one side and showing the change on the other.
  * Remember to provide any necessary test credentials for the third-party service in the 'Comments or questions on installation' field of your App Readiness Form, if this does not violate the agreement on application development with a third-party service. In other cases, a screen recording will suffice.
* Showcase your app's error handling and robust behavior in various scenarios: Do not limit your demonstration to ideal situations.
  * Invalid Inputs: Show how your app responds to incorrect input, such as negative numbers in price fields or unusual characters. The app should provide clear error messages and avoid crashing.
  * Common Scenarios: Demonstrate your app's functionality with diverse data types, including free products, products with variations, or large images.

#### Step 4: UI/UX & Responsive Design (approximately 1 minute)

* Demonstrate your app's visual appeal and usability across different devices.
* Open your browser's Developer Tools (F12) and activate the device toolbar.
* Select a mobile device (e.g., an iPhone 12 Pro) and show how your app's layout adapts, maintaining full usability on a smaller screen.

#### Step 5: Security & Data Handling

* Throughout your demonstration, articulate your app's security measures: "All our API communication is encrypted using HTTPS, and we never expose secret keys or access tokens on the client-side. Our Privacy Policy link is conveniently located in the app's footer. We are fully GDPR compliant and have a clear process for addressing merchant data requests."

#### Step 6: Uninstallation & Cleanup (approximately 1 minute)

* Demonstrate responsible development practices by leaving the store in a clean state.
* Navigate to Apps > My Apps in the Ecwid Control Panel and uninstall your app.
* Provide proof of cleanup:
  * **Storefront**: If your app added any elements to the storefront, revisit it to confirm their removal.
  * **Backend**: Explain your server's actions upon uninstallation: "When a merchant uninstalls, we receive a webhook from Ecwid. Our system then automatically deletes all their associated data, including their access token, from our database."

#### Step 7: Conclusion (approximately 20 seconds)

* State the end of your app's demo by sharing contact information: "This concludes the validation walkthrough for \[Your app's name]. Should you have any questions, please do not hesitate to contact us at \[your support email address]."

By following these steps, you will create a compelling screencast that effectively showcases your app and expedites its approval process.

\
