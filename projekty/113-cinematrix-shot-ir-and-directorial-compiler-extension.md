# P113 Extension — CineMatrix Shot IR & Directorial Compiler

## Parent
P113 — OmniVisual Prompt Compiler & Virtual Art Direction Engine MAX

## New capability
The CineMatrix corpus supplies a concrete cinematic intermediate representation between narrative intent and model-specific generation.

## Compiler chain

`MASTER SCENE → DIRECTORIAL INTENT → SHOT IR → CAMERA/LIGHT/ACTION PARAMETERS → MODEL ADAPTER → WORKFLOW → RENDER`

## Shot semantics
The compiler should represent shot type, lens, movement, camera angle, depth of field, lighting, color language, subject/location references, action, dialogue, duration, FPS, start/end frame and verification requirements.

## Important boundary
Cinematic parameters shown in the source are examples and source claims. They must not be hard-coded as universal Wan 2.1 truth. Adapter metadata must carry model/version-specific ranges and verification state.

## Continuity
Shot IR must reference stable character, location, prop and previous/next-shot entities rather than embedding identity only in free-text prompts.

## Status
`ARCHITECTURE ENHANCED — COMPILER IMPLEMENTATION NOT VERIFIED`
