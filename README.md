# Evolutionary-GPT2-Pruning: Layer-Wise Structural Compression

This project addresses the **AI scalability crisis** by automating the structural compression of Large Language Models. Using a **Genetic Algorithm (GA)**, the system autonomously discovers the optimal pruning strategy for GPT-2, significantly outperforming traditional uniform methods.

## Key Highlights

* **Sparsity Achievement**: Successfully reached **45% sparsity** while maintaining a stable perplexity of **~120**.
* **Performance vs. Baseline**: Outperformed uniform pruning, which led to model incoherence (perplexity **>250**) at the same sparsity level.
* **Structural Discovery**: The algorithm identified an **"Inverted U" pruning profile**, protecting syntactic layers while aggressively compressing redundant intermediate blocks.
* **Optimized Strategy**: Implemented a GA with **Strong Elitism (50%)** to ensure monotonic convergence despite limited computational resources.

## The Challenge: The "Cliff of Death"

Standard model optimization focuses on weight training in continuous spaces. However, structural pruning is a **discrete combinatorial problem**: deciding which neurons to keep (1) or remove (0).

Naive approaches (uniform pruning) often hit what is known as the **"Cliff of Death"**—a threshold (typically 30-35% for GPT-2) where model coherence collapses exponentially. Our approach treats the architecture as a dynamic system to bypass this limit.

## Technical Implementation

### Evolutionary Strategy

The goal was to determine the optimal pruning rate vector  across the 12 layers of GPT-2:

1. **Encoding**: Each individual in the population is a 12-dimensional vector.
2. **Fitness Evaluation**: Measured exclusively via **Perplexity**; lower values indicate better conservation of the model's cognitive capabilities.
3. **Genetic Operators**:
* **Strong Elitism**: 50% of the best individuals are retained without modification.
* **Bounded Mutation**: Variations are capped at 10% to refine solutions without destroying promising structures.

## Results & Analysis

| Method | Target Sparsity | Perplexity Score | Model Status |
| :--- | :---: | :---: | :--- |
| **Baseline (Original GPT-2)** | 0% | ~35-40 | Fully Functional |
| **Uniform Pruning** | 45% | > 250 | Incoherent / "Cliff of Death" |
| **Evolutionary GA (This Project)** | **45%** | **~ 120** | **Functional & Stable** |

The GA successfully "sacrificed" layers **L5, L6, and L10**, identifying high semantic redundancy or "dead" neurons. Conversely, it "protected" initial layers (**L0, L2, L4**) essential for processing input embeddings and syntax.

## Repository Structure
1. `notebooks/`:
* **Project Notebook**: Contains the full Python implementation, the GA loop, and model evaluation metrics.
3. `reports/`:
* **Complete Project Report (PDF)**: Detailed theoretical framework and empirical analysis.
* **Final Presentation (PPT)**: Summary of results and visual performance curves.

## References

It builds upon key research including:

1. Liu, S. et al. (2025). Beyond One-Size-Fits-All Pruning via Evolutionary Metric Search for Large Language Models. ArXiv:2502.10735.
2. Wang, C. et al. (2025). When Large Language Models Meet Evolutionary Algorithms: Potential Enhancements and Challenges. ArXiv:2401.10510.
3. Lang, J. et al. (2024). A Comprehensive Study on Quantization Techniques for Large Language Models. ArXiv:2411.02530.
4. Wu, S. et al. (2025). EvoP: Robust LLM Inference via Evolutionary Pruning. ArXiv:2502.14910.
5. Huang, W. et al. (2025). Towards Efficient Automatic Self-Pruning of Large Language Models. ArXiv:2502.14413.
