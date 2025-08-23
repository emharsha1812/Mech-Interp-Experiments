# Recall vs Reasoning Circuit Specialization

This directory contains experimental code and results for investigating circuit specialization in large language models (LLMs) for recall versus reasoning tasks. The research tests the hypothesis that LLMs develop distinct internal circuits for memory retrieval (recall) vs logical inference (reasoning) tasks.

## Research Overview

**Primary Hypothesis**: Large language models develop distinct internal circuits for recall (memory retrieval) vs reasoning (logical inference) tasks, with measurable differences in attention patterns, MLP activations, and information flow.

### Sub-Hypotheses Tested

- **H1**: Specific layers specialize for recall vs reasoning (layer specialization)
- **H2**: Attention heads show differential activation patterns between task types  
- **H3**: MLP neurons exhibit task-specific firing patterns
- **H4**: Circuit specialization is consistent across different model architectures *(Future work)*
- **H5**: Interventions on identified circuits selectively impair corresponding capabilities *(Future work)*

## Files Structure

### Notebooks

1. **`layers_and_attention_specialization.ipynb`** - Tests H1 and H2
   - Layer-level specialization analysis (H1)
   - Attention head differential patterns (H2)
   - Cross-validation framework
   - Statistical significance testing

2. **`MLP_activations_revised_v1.ipynb`** - Tests H3
   - MLP neuron task-specificity analysis
   - GPU-optimized processing for 530,432 neurons
   - Statistical validation with multiple testing correction

3. **`README.md`** - This documentation file

## Experimental Design

### Task Creation
- **Controlled Pairs**: 30 matched recall-reasoning task pairs
- **Recall Tasks**: Direct factual retrieval ("What is the capital of Switzerland?")
- **Reasoning Tasks**: Logical inference requiring multi-step processing ("If X is the capital of Switzerland and Switzerland is in Europe, what continent is X in?")

### Model Architecture
- **Target Model**: Qwen/Qwen2.5-7B-Instruct
- **Analysis Scope**: 28 layers, 28 attention heads per layer, 18,944 MLP neurons per layer
- **Total Components**: 784 attention heads, 530,432 MLP neurons

### Statistical Framework
- **Significance Level**: α = 0.01 (layers), α = 0.0001 (heads/neurons)
- **Effect Size**: Cohen's d > 0.8 (layers), d > 1.0 (heads/neurons)
- **Multiple Testing**: Benjamini-Hochberg correction
- **Cross-Validation**: 5-fold validation for robustness

## Key Results

### H1: Layer Specialization ✅ **SUPPORTED**
- **18/28 layers (64%)** show significant specialization
- **Recall-specialized layers**: [3,4,5,6,8,9,10,11,12,13,14,15,17,19,25] (15 layers)
- **Reasoning-specialized layers**: [1,2,18] (3 layers)
- **Cross-validation consistency**: 100%
- **Statistical significance**: p < 0.01, Cohen's d > 0.8

### H2: Attention Head Specialization ✅ **SUPPORTED**
- **583 attention heads** consistently specialized across validation
- **Recall-specialized**: 239 heads
- **Reasoning-specialized**: 219 heads
- **Mixed specialization**: 125 heads
- **Effect sizes**: 2.8-13.8 (mean: 6.83)
- **Top recall heads**: L2H5, L7H1, L6H9
- **Top reasoning heads**: L26H5, L27H8, L21H10

### H3: MLP Neuron Task-Specificity ✅ **SUPPORTED**
- **163,058/530,432 neurons (30.74%)** show task-specificity
- **Recall-specialized**: 79,221 neurons
- **Reasoning-specialized**: 83,837 neurons
- **Cross-validation consistent**: 50 neurons
- **Most specialized layer**: Layer 4 (11,857 neurons, 62.59%)
- **Statistical significance**: p < 0.001, Cohen's d > 0.5



## 🔍 Novel Findings

### Early Reasoning Hypothesis
Our analysis reveals a novel **"Early Reasoning Hypothesis"**: reasoning-specialized components are concentrated in early layers (1-2) and late layers (18, 26-27), suggesting:
- **Early layers**: Initial logical structure detection
- **Late layers**: Final reasoning synthesis
- **Middle layers**: Predominantly recall-specialized for fact retrieval

### Circuit Architecture
The results suggest a hierarchical circuit organization:
1. **Input Processing** (Layers 1-2): Reasoning pattern detection
2. **Memory Retrieval** (Layers 3-19): Fact extraction and recall
3. **Integration** (Layers 20-27): Reasoning synthesis and output

##  Technical Details

### Computational Requirements
- **GPU**: Recommended A100 or equivalent for H3 analysis
- **Memory**: 16GB+ GPU memory for full model analysis
- **Runtime**: ~30 minutes total for all experiments

### Data Collection
- **Activation Extraction**: Hidden states, attention weights, MLP outputs
- **Feature Engineering**: Norms, means, entropy, concentration, sparsity
- **Statistical Testing**: Mann-Whitney U, t-tests, effect sizes

##  Related Work

This research builds upon:
- Mechanistic interpretability frameworks (Anthropic, Redwood Research)
- Circuit analysis methodologies (Olah et al.)
- Task-specific neural specialization studies

##  Future Directions

### H4: Cross-Architecture Validation
- Test specialization patterns across different model families
- Investigate scaling effects (7B vs 70B parameters)

### H5: Causal Interventions
- Ablation studies on identified circuits
- Targeted interventions to validate causal relationships

### Extensions
- Multi-modal reasoning vs recall
- Temporal dynamics of circuit activation
- Fine-tuning effects on specialization patterns


## 🤝 Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Add comprehensive tests
4. Submit a pull request

## 📧 Contact

For questions or collaboration opportunities, please reach out via the main repository issues or discussions.

---
