# SmilesManager

A high-performance, responsive JavaScript utility for automatically rendering chemical SMILES strings into crisp SVGs using either **RDKit.js** or **SmilesDrawer**.

## Features

- **Auto-Discovery**: Uses `MutationObserver` to automatically detect and render any `[data-smiles]` elements added to the DOM (including modals and AJAX content).
- **Dual Engine Support**: Switch between the industry-standard RDKit (WASM) and the lightweight SmilesDrawer.
- **Dynamic Dependency Loading**: Automatically injects required scripts and Google Fonts only when needed.
- **High-Definition Rendering**: Implements "supersampling" by rendering at 2x resolution and using `geometricPrecision` CSS to eliminate pixelation and jagged lines.
- **Responsive Design**: Automatically detects parent container dimensions and scales SVGs to fit without overflowing.
- **Zero Configuration Setup**: Works out of the box with sensible defaults but remains fully customizable.

## Quick Start

1. Include the `smiles-render.js` script in your project.
2. Add a container with a `data-smiles` attribute:

```html
<div data-smiles="CC(=O)Oc1ccccc1C(=O)O"></div>
```

## Optional Configuration

### Global Initialization

You can overwrite the default settings by calling `initSmilesRender` in your own script:
```javascript
document.addEventListener('DOMContentLoaded', () => {
    SmilesManager.initSmilesRender(300, 150, 'rdkit', {
        bondLineWidth: 2.0,
        fixedBondLength: 15,
        padding: 0.05
    });
});
```

### Per-Element Overrides

You can customize specific molecules using `data-*` attributes:

```html
<div 
    data-smiles="CN1C=NC2=C1C(=O)N(C(=O)N2C)C" 
    data-engine="smiles-drawer" 
    data-width="400" 
    data-height="400">
</div>
```

## API Reference

### SmilesRender.initSmilesRender(width, height, engine, options)


| Parameter | Type   | Default | Description                                                       |
|-----------|--------|---------|-------------------------------------------------------------------|
| width     | Number | 200     | Default width for the rendered SVG.                               |
| height    | Number | 200     | Default height for the rendered SVG.                              |
| engine    | String | 'rdkit' | The rendering engine to use (rdkit or smiles-drawer).             |
| options   | Object | {}      | Drawing details like bondLineWidth, fixedBondLength, and padding. |

## Technical Details
- RDKit Integration: Specifically handles WASM initialization and requires strict integer types for JSON 
configuration to ensure vector clarity.

 - CSS Injection: Automatically injects a `<style>` block to handle .smiles-container alignment and `.smiles-svg` responsiveness.

 - SVG Optimization: Uses `preserveAspectRatio="xMidYMid meet"` and `shape-rendering: geometricPrecision` for the sharpest 
 possible output on High-DPI screens.

## Dependencies
The script dynamically loads the following if they are not already present:

RDKit: https://unpkg.com/@rdkit/rdkit/dist/RDKit_minimal.js

SmilesDrawer: https://unpkg.com/smiles-drawer@2.3.0/dist/smiles-drawer.min.js

Google Fonts: https://fonts.googleapis.com/css?family=Droid+Sans:400,700 (Droid Sans, required for SmilesDrawer labels)

## License
MIT