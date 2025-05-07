# Step-by-Step Guide: Building the Voice Translator App in MIT App Inventor

This guide provides instructions on how to construct the Voice Translator application using MIT App Inventor, based on the provided screenshots.

## Step 1: Project Setup

1.  Navigate to the MIT App Inventor website (appinventor.mit.edu) and log in.
2.  Click **Projects** > **Start new project**.
3.  Enter a project name (e.g., `VoiceTranslator`) and click **OK**.

## Step 2: Designing the User Interface (Designer View)

Switch to the **Designer** view.

1.  **Add Translation Direction Buttons:**
    * From the **Palette** > **User Interface**, drag two **`Button`** components onto the Viewer.
    * **Button 1 (English to French):**
        * Select the first `Button`.
        * In the **Properties** pane, set **`Text`** to `English to French`.
        * *Optional but Recommended:* Rename the component to `ButtonEnToFr`.
    * **Button 2 (French to English):**
        * Select the second `Button`.
        * In Properties, set **`Text`** to `French to English`.
        * *Optional:* Rename to `ButtonFrToEn`.

2.  **Add Labels for Text Display:**
    * From the **Palette** > **User Interface**, drag two **`Label`** components onto the Viewer, placing them below the buttons.
    * **Label 1 (Recognized Text):**
        * Select the first `Label`.
        * In Properties, set **`Text`** to `Translation Of French` (or an empty string, the screenshot shows example text).
        * Set **`TextColor`** to `Red`.
        * *Optional:* Rename to `LabelRecognizedText`.
    * **Label 2 (Translated Text):**
        * Select the second `Label`.
        * In Properties, set **`Text`** to `Translation of English` (or an empty string).
        * Set **`TextColor`** to `Cyan` (or Light Blue).
        * *Optional:* Rename to `LabelTranslatedText`.

3.  **Add Non-visible Components:**
    * From the **Palette** > **Media**, drag a **`SpeechRecognizer`** component onto the Viewer.
    * From the **Palette** > **Media**, drag a **`TextToSpeech`** component onto the Viewer.
    * From the **Palette** > **Experimental**, drag a **`YandexTranslate`** component onto the Viewer.

4.  **Configure YandexTranslate:**
    * Select the `YandexTranslate1` component.
    * In the **Properties** pane, enter your **`ApiKey`** obtained from Yandex Cloud. **This is crucial for translation to work.**

Your Designer view should now contain the buttons, labels, and the non-visible components as shown in the screenshot. The background color in the screenshot is black, you can set the `Screen1` background color to `Black` in its properties if you wish to match it.

## Step 3: Programming the App Logic (Blocks Editor)

Click the **Blocks** button in the top right corner to switch to the Blocks Editor.

1.  **Initialize Global Variable:**
    * Click on **Built-in** > **Variables**. Drag out the **`initialize global name to`** block.
    * Change `name` to `lang`.
    * Click on **Built-in** > **Math**. Drag out a **`number`** block (with `0`) and snap it into the `to` socket. *Note:* The screenshot shows initializing to `5`, but the logic uses `0` for En->Fr and `1` for Fr->En. Initialize to `0` or `1` depending on your preferred default, or handle the initial state differently. The blocks logic uses `0` and `1`. Let's initialize to `0` to match the En->Fr button's initial state setting.

2.  **English to French Button Logic:**
    * Click on `ButtonEnToFr` (or your renamed button). Drag out the **`when ButtonEnToFr.Click do`** block.
    * Inside this block:
        * Click on `SpeechRecognizer1`. Drag out the **`call SpeechRecognizer1.GetText`** block. This starts listening for speech.
        * Click on **Built-in** > **Variables**. Drag out the **`set global lang to`** block.
        * Click on **Built-in** > **Math**. Drag out a **`number`** block (with `0`) and snap it into the `to` socket. (0 represents English to French).

3.  **French to English Button Logic:**
    * Click on `ButtonFrToEn` (or your renamed button). Drag out the **`when ButtonFrToEn.Click do`** block.
    * Inside this block:
        * Click on `SpeechRecognizer1`. Drag out the **`call SpeechRecognizer1.GetText`** block.
        * Click on **Built-in** > **Variables**. Drag out the **`set global lang to`** block.
        * Click on **Built-in** > **Math**. Drag out a **`number`** block (with `1`) and snap it into the `to` socket. (1 represents French to English).

4.  **After Speech Recognition Logic:**
    * Click on `SpeechRecognizer1`. Drag out the **`when SpeechRecognizer1.AfterGettingText result partial do`** block.
    * Inside this block, we need an `if/else if` structure to handle the translation based on the `lang` variable.
    * Click on **Built-in** > **Control**. Drag out an **`if then`** block.
    * Click on the blue gear icon on the `if then` block and drag an **`else if`** block into it, then click the gear again to close.
    * **Condition for English to French:**
        * Click on **Built-in** > **Logic**. Drag out the **`=`** comparison block.
        * Click on **Built-in** > **Math**. Drag out a **`number`** block (with `0`). Snap it into the first socket of the `=` block.
        * Click on **Built-in** > **Variables**. Drag out the **`get global lang`** block and snap it into the second socket of the `=` block.
        * Snap the entire `=` block into the `if` condition socket.
    * **If English to French (lang = 0):**
        * Click on `YandexTranslate1`. Drag out the **`call YandexTranslate1.RequestTranslation languageToTranslateTo textToTranslate`** block and place it inside the `then` part of the `if` block.
        * Click on **Built-in** > **Text**. Drag out a **`text`** block (with empty quotes). Type `fr` inside the quotes and snap it into the `languageToTranslateTo` socket.
        * Hover over the `result` variable in the `AfterGettingText` block header, select **`get result`**, and snap it into the `textToTranslate` socket.
        * Click on `LabelRecognizedText` (or your renamed label). Drag out the **`set LabelRecognizedText.Text to`** block.
        * Hover over the `result` variable, select **`get result`**, and snap it into the `set LabelRecognizedText.Text` block.
    * **Condition for French to English:**
        * Click on **Built-in** > **Logic**. Drag out the **`=`** comparison block.
        * Click on **Built-in** > **Math**. Drag out a **`number`** block (with `1`). Snap it into the first socket of the `=` block.
        * Click on **Built-in** > **Variables**. Drag out the **`get global lang`** block and snap it into the second socket of the `=` block.
        * Snap the entire `=` block into the `else if` condition socket.
    * **If French to English (lang = 1):**
        * Click on `YandexTranslate1`. Drag out the **`call YandexTranslate1.RequestTranslation languageToTranslateTo textToTranslate`** block and place it inside the `then` part of the `else if` block.
        * Click on **Built-in** > **Text**. Drag out a **`text`** block (with empty quotes). Type `en` inside the quotes and snap it into the `languageToTranslateTo` socket.
        * Hover over the `result` variable, select **`get result`**, and snap it into the `textToTranslate` socket.
        * Click on `LabelRecognizedText`. Drag out the **`set LabelRecognizedText.Text to`** block.
        * Hover over the `result` variable, select **`get result`**, and snap it into the `set LabelRecognizedText.Text` block.

5.  **After Translation Logic:**
    * Click on `YandexTranslate1`. Drag out the **`when YandexTranslate1.GotTranslation responseCode translation do`** block. This block runs when the translation service returns a result.
    * Inside this block:
        * Click on `TextToSpeech1`. Drag out the **`call TextToSpeech1.Speak message`** block.
        * Hover over the `translation` variable in the `GotTranslation` block header, select **`get translation`**, and snap it into the `message` socket.
        * Click on `LabelTranslatedText` (or your renamed label). Drag out the **`set LabelTranslatedText.Text to`** block.
        * Hover over the `translation` variable, select **`get translation`**, and snap it into the `set LabelTranslatedText.Text` block.

Arrange your blocks neatly in the workspace. Your blocks should now look similar to the screenshot provided.

## Step 4: Testing the Application

1.  In the App Inventor web interface, click **Connect** in the top menu.
2.  Choose either "AI Companion" (recommended for devices with microphones) or "Emulator" (if configured for audio input).
3.  Ensure your device/emulator has a working internet connection and microphone.
4.  Tap the "English to French" or "French to English" button.
5.  When prompted, speak clearly into the microphone.
6.  Observe the recognized text appear, then the translated text appear and be spoken aloud.

You have successfully built the Voice Translator application! Remember that the accuracy of the translation depends on the Yandex Translate service and the clarity of the speech input.
