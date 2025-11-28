# UI-Inversion-Shader-for-Unity
A Unity shader that creates a clean color inversion effect for UI elements by sampling and inverting the background screen colors. 

## Features

- **Clean Color Inversion**: Inverts background colors where UI elements are rendered
- **Sharp Text Rendering**: Uses step function for crisp, anti-aliasing-free text edges
- **Universal Render Pipeline (URP)**: Designed for Unity's URP
- **UI System Integration**: Full support for Unity's Canvas system with stencil and clipping
- **Transparent Background**: Only shows inverted colors where UI elements exist

## Requirements

- Unity 2021.3 or later (Unity 6 compatible)
- Universal Render Pipeline (URP)
- URP Opaque Texture enabled in your URP settings

## Installation

1. Copy `UI_Inversion.shader` to your Unity project's `Assets/Shaders/` folder

2. Enable Opaque Texture in your URP Renderer settings:
   - Select your URP Renderer asset
   - Check **"Opaque Texture"** under Camera settings

3. Create a new Material using this shader

4. Apply the material to UI elements (Image, Text, etc.)

## Usage

### Basic Setup

1. Create a new Material in Unity
2. Set the shader to `UI/Inversion`
3. Assign the material to any UI Image or Text component
4. The UI element will now display inverted colors of whatever is behind it

### Properties

| Property | Description |
|----------|-------------|
| **Sprite Texture** | The texture/sprite to use as a mask (auto-assigned for UI) |
| **Tint** | Color tint applied to the effect |
| **Stencil Settings** | Standard UI stencil properties for masking and layering |
| **Use Alpha Clip** | Enables alpha clipping for UI elements |

## Technical Details

### How It Works

1. **Screen Sampling**: Captures the screen texture behind the UI element using `_CameraOpaqueTexture`
2. **Color Inversion**: Inverts RGB values using `1.0 - screenColor.rgb`
3. **Masking**: Uses the UI texture's alpha channel as a mask with sharp cutoff (step function at 0.5)
4. **Output**: Renders inverted colors where the mask exists, transparent elsewhere

### Shader Features

- Vertex/Fragment shader with HLSL
- Multi-compile support for UI clipping and alpha clip
- Sharp texture sampling for clean text rendering
- Screen position computation for background sampling
- Full stencil buffer support

### Important Notes

 **This shader is UI-specific** and designed for Unity's Canvas system  
 Will not work with 3D objects without modification  
 Requires URP Opaque Texture to be enabled  
 Uses shader target 2.0 for broad compatibility

## Performance

-  Lightweight and optimized for UI rendering
-  Minimal texture samples (1 UI texture + 1 screen texture)

## Troubleshooting

### UI appears black or transparent
- Ensure **Opaque Texture** is enabled in your URP Renderer settings
- Check that you're using a URP Renderer, not Built-in Pipeline

### Text appears blurry
- This shader uses sharp cutoff for crisp edges
- Adjust the alpha threshold in line 124 if needed

### Colors aren't inverting
- Verify the shader is receiving the correct screen texture
- Check that the UI element has proper alpha values in its texture

## License

This project is licensed under the MIT License 
