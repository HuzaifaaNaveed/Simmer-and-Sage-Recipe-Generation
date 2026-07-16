# Simmer and Sage 🍲

**A finetuned language model for generating authentic Pakistani and Indian recipes.**

Simmer and Sage is a generative AI system that finetunes a compact language model (LFM2 1.2B) on curated Pakistani and Indian recipes to generate authentic, structured recipes from a simple dish name. It exists to bridge the gap between encountering an unfamiliar desi dish and actually knowing how to cook it, from hostel stoves to home tandoors.

## Overview

Many people run into Pakistani and Indian dishes they don't know how to make, and most general-purpose recipe tools aren't trained on authentic South Asian ingredients, techniques, or spice profiles. Simmer and Sage solves this by finetuning a compact language model exclusively on curated Pakistani and Indian recipe data, then serving it through a clean web interface.

## Features

- **Text-to-recipe generation** — enter a dish name, get a full recipe back
- **Culturally authentic output** — trained exclusively on Pakistani and Indian recipes for accurate ingredients, spice levels, and cooking methods
- **Structured JSON output** — recipes are generated in a strict JSON schema (dish name, ingredients array, directions array), enabling 100% reliable parsing with zero extraction errors
- **Fast inference** — under 5 seconds per recipe

## Tech Stack

- [LFM2 1.2B](https://www.liquid.ai/) by Liquid AI as the base model
- Adapter-based finetuning (LoRA-style) via [Unsloth](https://github.com/unslothai/unsloth) for efficient training on free-tier Colab GPUs
- Custom JSON-formatted finetuning pipeline for consistent, machine-parseable output

## How It Works

1. A dish name is passed as input to the model
2. The finetuned adapter is loaded and merged with the base LFM2 model
3. Inference runs on GPU, generating a JSON-formatted recipe (dish name, ingredients, directions)
4. The structured JSON output is directly parseable — no post-processing or extraction logic required

## Dataset & Training Approach

- Started from multimodal recipe datasets (RecipeQA, Food Ingredients and Recipes with Images) but pivoted to **text-to-text** generation after image-to-recipe proved computationally infeasible on available hardware
- Filtered all training data down to **Pakistani and Indian recipes only** for cultural relevance and authenticity
- Converted all recipe data into a standardized **JSON schema** ahead of finetuning to guarantee parseable, structured output
- Used adapter-based finetuning (rather than full finetuning) to keep training lightweight, fast, and feasible within Colab's free-tier GPU limits

## Evaluation

Recipes were evaluated both qualitatively and quantitatively:

- **Qualitative:** coherence, culinary realism, alignment with the input query, cultural appropriateness, and completeness — assessed by human reviewers
- **Quantitative:** ingredient similarity matching, step clarity, JSON output validity (100% parse success), and inference latency

## Limitations

- Colab's GPU runtime cap limited training duration and dataset size
- High-quality structured Pakistani/Indian recipe data is scarce and was sourced primarily from public online resources
- LFM2 1.2B is a relatively small model; larger models could improve recipe depth and diversity
- Currently text-only — no image-to-recipe support yet

## Future Work

- [ ] Image-to-recipe generation 
- [ ] Larger base models 
- [ ] Broader regional coverage 
- [ ] Dietary and preference controls 
- [ ] Nutritional information 
