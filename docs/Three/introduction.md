# Three.js

Three.js is a JavaScript library for creating 3D content on the web.

## Common Materials

- MeshBasicMaterial
- MeshNormalMaterial
- MeshPhongMaterial
- MeshStandardMaterial

## Differences between Common Materials

| Material             | Require Lighting | Reflection       | Shading                                            | Performance |
| -------------------- | ---------------- | ---------------- | -------------------------------------------------- | ----------- |
| MeshBasicMaterial    | None             | None             | Flat                                               | High        |
| MeshNormalMaterial   | None             | None             | Normal vectors (rendered based on camera position) | High        |
| MeshPhongMaterial    | Yes              | Basic            | Smooth                                             | Medium      |
| MeshStandardMaterial | Yes              | Physically-Based | Smooth                                             | Medium      |

## Lights

### Common Light Types

- **AmbientLight**: Provides a uniform light across the entire scene without any direction.
- **DirectionalLight**: Simulates sunlight, providing light from a fixed direction regardless of its position, and can cast shadows.
- **PointLight**: Emits light in all directions from a single point, similar to a light bulb.
- **SpotLight**: Emits a cone of light in a specific direction, useful for highlighting specific areas or objects.

### Differences between Common Light Types

| Light Type       | Shadows | Direction | Intensity Control | Performance |
| ---------------- | ------- | --------- | ----------------- | ----------- |
| AmbientLight     | No      | None      | Low               | High        |
| DirectionalLight | Yes     | Fixed     | High              | Medium      |
| PointLight       | Yes     | Radial    | High              | Medium      |
| SpotLight        | Yes     | Cone      | High              | Low         |

### Example Image

![Common Light Types in Three.js](https://willievaldez.github.io/assets/img/light_types.png)

## Shadows

> [!IMPORTANT]  
> Enable shadows in the renderer:
>
> ```javascript
> renderer.shadowMap.enabled = true;
> ```

> [!IMPORTANT]  
> Set the `castShadow` property to `true` for lights that you want to cast shadows:
>
> ```javascript
> directionalLight.castShadow = true;
> pointLight.castShadow = true;
> spotLight.castShadow = true;
> ```

### Common Shadow Map Types

- **BasicShadowMap**: Unfiltered shadow maps. Fastest, but lowest quality.
- **PCFShadowMap**: Uses Percentage-Closer Filtering (PCF) algorithm to filter shadow maps. Default setting.
- **PCFSoftShadowMap**: Uses Percentage-Closer Soft Shadows (PCSS) algorithm to filter shadow maps for softer shadows.
- **VSMShadowMap**: Uses Variance Shadow Map (VSM) algorithm to filter shadow maps. All shadow receivers will also cast shadows with this setting.

_Note created by s1n7ax on 2025-02-26 15:56:14 (UTC)._
