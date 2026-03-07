# Perplexities Demystified
>[!NOTE]
After researching problems and finding workarounds, I instruct AI to build simple demos and ensure the code is commented sufficiently to explain solution.

## CSS Typed OM, Custom Properties and attributeStyleMap

Current browsers appear to have a limitation where they don't yet accept `CSS.number()` or `CSSKeywordValue()` when using `attributeStyleMap.set()` specifically for custom CSS properties (--*), even when registered via `@property`. 

See the code (or screenshot below) where the properties are set as strings (which the browser accepts and handles properly under the hood).

Use `delete()` to safely revert to the default. The reading side of Typed OM still perfectly returns a true Number object because of the @property definitions!

<p align="center">
  <img 
    src="./assets/Typed-OM-And-AttributeStyleMap.webp" 
    alt=`<!-- Generated with the help of Google Gemini -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="generator" content="Google Gemini">
    <title>Houdini Typed OM Fonts</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap" rel="stylesheet">
    <style>
        /* 1. Define custom properties */
        @property --font-weight-axis {
            syntax: '<number>';
            inherits: false;
            initial-value: 400;
        }

        @property --font-slant-axis {
            syntax: '<number>';
            inherits: false;
            initial-value: 0;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: #0f172a;![Typed-OM-And-AttributeStyleMap](https://github.com/user-attachments/assets/3fe63d3a-d5ef-4640-a14a-c9c0344174ff)

            color: #f8fafc;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 3rem 1rem;
        }

        .variable-text {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            transition: font-variation-settings 0.5s ease;
            font-variation-settings: "wght" var(--font-weight-axis), "slnt" var(--font-slant-axis);
        }

        .controls {
            display: flex;
            gap: 1rem;
            margin-top: 2rem;
        }

        button {
            padding: 0.75rem 1.5rem;
            border-radius: 0.5rem;
            border: none;
            background-color: #3b82f6;
            color: white;
            font-weight: 600;
            cursor: pointer;
        }

        .reset-btn { background-color: #ef4444; }
        
        #current-values {
            margin-top: 2rem;
            font-family: monospace;
            color: #94a3b8;
        }
    </style>
</head>
<body>

    <div class="variable-text" id="target-text">Typed OM is awesome</div>

    <div class="controls">
        <button onclick="setTypedValues()">Set Typed Values</button>
        <button class="reset-btn" onclick="resetUsingTypedOM()">Reset to Initial</button>
    </div>
    
    <div id="current-values">Weight: 400 | Slant: 0</div>

    <script>
        const textElement = document.getElementById('target-text');
        const output = document.getElementById('current-values');

        function setTypedValues() {
            const randomWeight = Math.floor(Math.random() * 800) + 100;
            const randomSlant = Math.floor(Math.random() * -10);

            // BROWSER LIMITATION FIX:
            // While Typed OM is meant to avoid strings, current browser implementations 
            // reject `CSS.number()` and `new CSSKeywordValue()` for CUSTOM properties (--*). 
            // They require standard strings to be set, which Typed OM converts to CSSUnparsedValue internally.
            textElement.attributeStyleMap.set('--font-weight-axis', randomWeight.toString());
            textElement.attributeStyleMap.set('--font-slant-axis', randomSlant.toString());
            
            updateDisplay();
        }

        function resetUsingTypedOM() {
            // Because of the same browser limitation mentioned above, setting custom properties 
            // to a CSSKeywordValue('initial') throws an error.
            // The cleanest and most reliable way to reset a property in Typed OM is to delete the inline override entirely.
            textElement.attributeStyleMap.delete('--font-weight-axis');
            textElement.attributeStyleMap.delete('--font-slant-axis');

            updateDisplay();
        }

        function updateDisplay() {
            // THE REAL MAGIC IS HERE:
            // Even though we have to use strings to SET custom properties, because you used @property,
            // computing the styles READS them back as true numbers (CSSUnitValue) automatically!
            // No parseInt() or parseFloat() required.
            
            const weightObj = textElement.computedStyleMap().get('--font-weight-axis');
            const slantObj = textElement.computedStyleMap().get('--font-slant-axis');
            
            // Provide fallbacks to initial values if the objects are undefined for any reason
            const currentWeight = weightObj ? weightObj.value : 400;
            const currentSlant = slantObj ? slantObj.value : 0;
            
            output.innerText = `Weight: ${currentWeight} (Type: ${typeof currentWeight}) | Slant: ${currentSlant}`;
        }
    </script>
</body>
</html>` 
    title=`<!-- Generated with the help of Google Gemini -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="generator" content="Google Gemini">
    <title>Houdini Typed OM Fonts</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap" rel="stylesheet">
    <style>
        /* 1. Define custom properties */
        @property --font-weight-axis {
            syntax: '<number>';
            inherits: false;
            initial-value: 400;
        }

        @property --font-slant-axis {
            syntax: '<number>';
            inherits: false;
            initial-value: 0;
        }

        body {
            font-family: 'Inter', sans-serif;
            background-color: #0f172a;![Typed-OM-And-AttributeStyleMap](https://github.com/user-attachments/assets/3fe63d3a-d5ef-4640-a14a-c9c0344174ff)

            color: #f8fafc;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 3rem 1rem;
        }

        .variable-text {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            transition: font-variation-settings 0.5s ease;
            font-variation-settings: "wght" var(--font-weight-axis), "slnt" var(--font-slant-axis);
        }

        .controls {
            display: flex;
            gap: 1rem;
            margin-top: 2rem;
        }

        button {
            padding: 0.75rem 1.5rem;
            border-radius: 0.5rem;
            border: none;
            background-color: #3b82f6;
            color: white;
            font-weight: 600;
            cursor: pointer;
        }

        .reset-btn { background-color: #ef4444; }
        
        #current-values {
            margin-top: 2rem;
            font-family: monospace;
            color: #94a3b8;
        }
    </style>
</head>
<body>

    <div class="variable-text" id="target-text">Typed OM is awesome</div>

    <div class="controls">
        <button onclick="setTypedValues()">Set Typed Values</button>
        <button class="reset-btn" onclick="resetUsingTypedOM()">Reset to Initial</button>
    </div>
    
    <div id="current-values">Weight: 400 | Slant: 0</div>

    <script>
        const textElement = document.getElementById('target-text');
        const output = document.getElementById('current-values');

        function setTypedValues() {
            const randomWeight = Math.floor(Math.random() * 800) + 100;
            const randomSlant = Math.floor(Math.random() * -10);

            // BROWSER LIMITATION FIX:
            // While Typed OM is meant to avoid strings, current browser implementations 
            // reject `CSS.number()` and `new CSSKeywordValue()` for CUSTOM properties (--*). 
            // They require standard strings to be set, which Typed OM converts to CSSUnparsedValue internally.
            textElement.attributeStyleMap.set('--font-weight-axis', randomWeight.toString());
            textElement.attributeStyleMap.set('--font-slant-axis', randomSlant.toString());
            
            updateDisplay();
        }

        function resetUsingTypedOM() {
            // Because of the same browser limitation mentioned above, setting custom properties 
            // to a CSSKeywordValue('initial') throws an error.
            // The cleanest and most reliable way to reset a property in Typed OM is to delete the inline override entirely.
            textElement.attributeStyleMap.delete('--font-weight-axis');
            textElement.attributeStyleMap.delete('--font-slant-axis');

            updateDisplay();
        }

        function updateDisplay() {
            // THE REAL MAGIC IS HERE:
            // Even though we have to use strings to SET custom properties, because you used @property,
            // computing the styles READS them back as true numbers (CSSUnitValue) automatically!
            // No parseInt() or parseFloat() required.
            
            const weightObj = textElement.computedStyleMap().get('--font-weight-axis');
            const slantObj = textElement.computedStyleMap().get('--font-slant-axis');
            
            // Provide fallbacks to initial values if the objects are undefined for any reason
            const currentWeight = weightObj ? weightObj.value : 400;
            const currentSlant = slantObj ? slantObj.value : 0;
            
            output.innerText = `Weight: ${currentWeight} (Type: ${typeof currentWeight}) | Slant: ${currentSlant}`;
        }
    </script>
</body>
</html>`
    width="1188" 
    height="2502"
  />
</p>


