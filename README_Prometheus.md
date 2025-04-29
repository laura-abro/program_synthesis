# NEAR Program Synthesis: A Comprehensive Framework for Neural Program Generation and Research

## Project Overview

NEAR Program Synthesis is a comprehensive research framework designed to advance and standardize program synthesis techniques across multiple domains and programming challenges. The primary goal of this project is to provide researchers and developers with a unified platform for exploring, developing, and comparing program synthesis algorithms.

### Key Features
- Supports multiple program synthesis domains, including:
  - AlgoLisp: Algorithm synthesis using Lisp-like representations
  - Karel: A domain for synthesizing robot navigation and control programs
  - NAPS (Natural Program Synthesis): Advanced techniques for generating programs from natural language specifications

### Core Capabilities
- Modular architecture for developing and experimenting with program synthesis models
- Integrated datasets and evaluation tools across different program synthesis domains
- Implementations of advanced sequence-to-sequence and neural program synthesis techniques
- Support for model training, evaluation, and inference across various programming tasks

### Research and Development Benefits
- Facilitates comparative research in program synthesis
- Provides a standardized framework for developing and testing new program synthesis algorithms
- Enables researchers to explore machine learning approaches to automatic program generation
- Supports reproducibility and collaborative development of program synthesis techniques

## Getting Started, Installation, and Setup

### Prerequisites

- Python 3.5 or later
- pip package manager
- Basic understanding of machine learning and program synthesis concepts

### Installation

Install the project using pip:

```bash
pip install program-synthesis
```

#### Manual Installation

1. Clone the repository:
```bash
git clone https://github.com/nearai/program_synthesis.git
cd program_synthesis
```

2. Create a virtual environment (recommended):
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

3. Install dependencies:
```bash
pip install -r requires.txt
pip install .
```

### Dependencies

The project requires the following key dependencies:
- NumPy
- TensorFlow
- PyTorch (via torchfold)
- Boto3
- ipython
- gym
- pytest

### Quick Start

To use the program synthesis tools, you can import the relevant modules:

```python
from program_synthesis import algolisp, karel, naps

# Example usage will depend on the specific module and task
```

### Development Setup

1. For development, install additional testing dependencies:
```bash
pip install pytest pytest-timeout pytest-xdist
```

2. Run tests to verify installation:
```bash
pytest
```

### Platform Considerations

- This project is primarily designed for Unix-like systems (Linux, macOS)
- Windows users may need to use Windows Subsystem for Linux (WSL)
- Ensure compatibility with Python 3.5+ environments

### Troubleshooting

- Make sure you have the latest version of pip
- Check that all dependencies are correctly installed
- Verify Python version compatibility

## Dataset

The project uses a flexible dataset system for program synthesis tasks, with the following key characteristics:

### Dataset Structure
- Data is stored in JSON Lines (.jsonl) format
- Each data example includes:
  - Text description
  - Input/output tests
  - Code tree and code sequence
  - Function schemas
  - Language specification (default is Lisp)

### Dataset Variants
The system supports multiple datasets, with examples including:
- Metagen dataset (`data/generated/metaset3.*`)
- Flexible configuration for data loading and preprocessing

### Key Dataset Features
- Dynamic vocabulary generation
- Support for multiple programming languages
- Configurable dataset filtering
  - Maximum code length
  - Vocabulary frequency thresholds
  - Empty code filtering

### Data Example Schema
```json
{
  "text": ["description", "tokens"],
  "args": {"arg_name": "arg_type"},
  "return_type": "return_type",
  "code_sequence": ["code", "tokens"],
  "code_tree": ["nested", "code", "structure"],
  "tests": ["input", "output", "test", "cases"],
  "language": "lisp/uast"
}
```

### Preprocessing Capabilities
- Tokenization for text and code
- Dynamic placeholder handling
- Vocabulary generation with configurable frequency thresholds

## Model Architecture and Training

The project implements multiple sequence-to-sequence machine learning models for program synthesis across different domains (AlgoLisp, Karel, NAPS). The core architecture is a flexible neural network implementation focused on translating specifications or inputs into executable code.

### Model Architecture

The primary model architecture is a sequence-to-sequence (Seq2Seq) neural network with the following key components:

- **Encoder**: Uses specialized encoders for different input types:
  - Text encoder
  - I/O specification encoder
  - Code sequence encoder
  - Trace encoder

- **Decoder**: Implements beam search decoding with configurable beam size
  - Supports generating code sequences from encoded representations
  - Uses attention mechanisms for improved context understanding

### Training Strategy

The training process is implemented with the following characteristics:

- Uses PyTorch as the deep learning framework
- Supports multi-GPU and CUDA acceleration
- Implements adaptive learning techniques
- Provides extensive logging and monitoring during training

### Training Configuration

Key training parameters include:
- Configurable epochs
- Customizable learning rate
- Evaluation intervals
- Beam search configuration
- Support for multiple vocabulary sizes

### Training Command

To train the model, use the training script with appropriate arguments. The exact command depends on the specific domain and configuration. Typical invocation follows this pattern:

```bash
python -m program_synthesis.domain.train \
    --model_type seq2seq \
    --model_dir ./saved_models \
    --num_epochs 50 \
    --cuda
```

### Dependencies

The project requires the following key libraries:
- PyTorch
- NumPy
- torchfold
- TensorFlow (for some components)

### Model Variants

The implementation supports multiple model variants across domains:
- Seq2Seq model for AlgoLisp
- Karel programming environment models
- NAPS (Neural Program Synthesis) models

The flexible architecture allows adaptation to different programming synthesis tasks while maintaining a consistent underlying neural network structure.

## Evaluation and Results

### Evaluation Methodology

The model was evaluated using a comprehensive set of performance metrics designed to assess code generation and program synthesis capabilities. The evaluation process involved running inference on a development dataset and computing multiple performance indicators.

#### Key Performance Metrics

1. **BLEU Score**: Measures the similarity between generated code and ground truth code sequences, indicating the quality of code generation.

2. **Accuracy Metrics**:
   - **Exact Accuracy**: Percentage of programs that match the ground truth code exactly
   - **Full Test Accuracy**: Percentage of programs that pass all test cases
   - **Partial Accuracy (50% Test Pass)**: Percentage of programs that pass at least 50% of test cases

3. **Error Analysis**:
   - **Syntax Error Frequency**: Rate of programs with syntax errors
   - **Runtime Exception Frequency**: Rate of programs with runtime exceptions
   - **Other Exception Frequency**: Rate of other types of exceptions

#### Evaluation Process

The evaluation process involves the following key steps:
1. Run model inference on the development dataset
2. Execute generated code against predefined test cases
3. Compute performance metrics across the entire dataset

##### Metrics Computation
- Metrics are calculated by averaging performance across all generated programs
- Programs are executed and tested using a specialized code executor
- Comprehensive test suite evaluates both code correctness and performance

#### Reporting

Performance metrics are automatically logged during the evaluation process, providing detailed insights into the model's code generation capabilities. The evaluation tracks:
- Total number of programs generated
- Total number of tests executed
- Breakdown of program correctness and error types

### Performance Highlights

While specific performance numbers may vary depending on the exact dataset and configuration, the evaluation framework provides a robust mechanism for assessing program synthesis models across multiple dimensions of code generation quality.

## Inference / How to Use the Model

The model supports inference through a command-line interface with various configuration options.

### Inference Command

To run inference, use the `infer.py` script with the following key parameters:

```bash
python program_synthesis/karel/infer.py \
  --model_type MODEL_TYPE \
  --model_dir PATH_TO_MODEL_DIRECTORY \
  --infer_output OUTPUT_FILE \
  [optional arguments]
```

### Required Arguments

- `--model_type`: Specify the type of model (e.g., `karel-lgrl`)
- `--model_dir`: Path to the directory containing the trained model
- `--infer_output`: File path to save the inference results

### Optional Arguments

- `--cuda`: Enable GPU inference (automatically detected if CUDA is available)
- `--eval_final`: Use the final evaluation dataset
- `--eval_train`: Use the training dataset for evaluation
- `--infer_limit`: Limit the number of inference outputs

### Output

The inference generates two files:
- `OUTPUT_FILE`: Contains the pickled inference results
- `OUTPUT_FILE.index`: An index file for accessing the results

### Example Inference Command

```bash
python program_synthesis/karel/infer.py \
  --model_type karel-lgrl \
  --model_dir logdirs/karel-sgd-cl1-lr1-lds100k-ldr0.5 \
  --infer_output inference_results.pkl
```

### Important Notes

- Ensure you have a trained model before running inference
- The model must be compatible with the specified dataset
- GPU acceleration is recommended for faster inference

## Project Structure

The project is organized into several key directories and modules:

#### Main Project Structure
```
program_synthesis/
│
├── algolisp/       # AlgoLisp-specific implementation
├── common/         # Shared utilities and modules
├── conala/         # Conala-specific modules
├── karel/          # Karel programming environment modules
└── naps/           # NAPS (Universal Abstract Syntax Tree) modules
```

#### Key Directories and Their Purposes

##### `program_synthesis/common/`
Contains core shared utilities and modules used across different subprojects:
- `models/`: Base machine learning model components
- `modules/`: Reusable neural network modules (attention, encoders, decoders)
- `tools/`: Utility functions for logging, saving, and reporting

##### `program_synthesis/algolisp/`
Focuses on AlgoLisp implementation:
- `dataset/`: Data processing and handling
- `models/`: Specific model architectures for AlgoLisp
- `tools/`: AlgoLisp-specific utilities

##### `program_synthesis/karel/`
Karel programming environment implementation:
- `dataset/`: Karel-specific data processing
- `models/`: Karel programming models
- `notebooks/`: Experimental Jupyter notebooks
- `scripts/`: Utility scripts for evaluation and data manipulation

##### `program_synthesis/naps/`
Universal Abstract Syntax Tree (UAST) project:
- `examples/`: Example implementations (e.g., seq2seq)
- `pipelines/`: Data processing pipelines
- `pipes/`: Data transformation utilities
- `uast/`: Core UAST implementation and language conversion tools

#### Supporting Files
- `setup.py`: Project installation configuration
- `requires.txt`: Project dependencies
- `LICENSE`: Project licensing information

## Technologies Used

### Programming Languages
- Python 3.5+

### Machine Learning and Deep Learning Frameworks
- TensorFlow
- PyTorch (via torchfold)

### Core Libraries and Tools
- NumPy: Numerical computing
- Boto3: AWS SDK for Python
- TQDM: Progress bar for loops
- Prompt Toolkit: Interactive command line interfaces
- PLY (Python Lex-Yacc): Parsing tools

### Development and Testing
- pytest: Testing framework
- pytest-timeout: Test timeout management
- pytest-xdist: Parallel test execution

### Utility Libraries
- Cached Property: Decorator for computed properties
- Python-Levenshtein: String distance calculations
- Sorted Containers: Performant sorted data structures
- Gym: Reinforcement learning toolkit
- PyLRU: LRU caching
- PyParsing: Parsing library

### Additional Tools
- IPython: Enhanced interactive Python shell

## Additional Notes

### Research and Academic Context

This project represents a comprehensive framework for program synthesis research, offering multiple datasets and models to explore automated program generation techniques. The repository provides implementations across different programming domains and paradigms.

### Key Research Contributions

- Provides a unified infrastructure for comparing program synthesis algorithms
- Supports multiple datasets: AlgoLisp, Karel, and NAPS
- Enables reproducible research in machine learning-based program generation
- Implements advanced sequence-to-sequence and neural network architectures for program synthesis

### Experimental Limitations and Considerations

While the project offers robust research tools, users should be aware of:
- Experimental nature of program synthesis techniques
- Computational complexity of neural program generation
- Domain-specific constraints in each dataset

### Performance and Scalability

The framework is designed for research environments and may require significant computational resources:
- Recommended for environments with GPU acceleration
- Best suited for small to medium-sized program synthesis tasks
- Performance varies across different datasets and model configurations

### Future Research Directions

Potential areas for future exploration include:
- Extending model architectures
- Improving generalization across programming domains
- Developing more robust program synthesis techniques
- Creating new synthetic and real-world datasets

### Acknowledgments

This research was supported by the open-source community and represents a collaborative effort in advancing program synthesis techniques.

## Contributing

We welcome contributions to the Program Synthesis project! Here are some guidelines to help you get started:

### Ways to Contribute
- Reporting bugs
- Suggesting enhancements
- Improving documentation
- Adding new features
- Fixing existing issues

### Getting Started
1. Fork the repository
2. Create a new branch for your contribution
3. Make your changes
4. Ensure all tests pass
5. Submit a pull request

### Development Setup
- Use Python 3.5 or higher
- Create a virtual environment
- Install development dependencies with `pip install -e .`

### Code Guidelines
- Follow PEP 8 style guidelines
- Write clear, concise, and descriptive commit messages
- Include tests for new functionality
- Update documentation to reflect your changes

### Testing
- Run tests using `pytest`
- Ensure your code passes all existing tests
- Add new tests for any new functionality

### Reporting Issues
- Use the GitHub Issues section
- Provide a clear and descriptive title
- Include a detailed description of the issue
- If reporting a bug, include steps to reproduce, expected behavior, and actual behavior

### Pull Request Process
1. Ensure your code follows the project's coding standards
2. Update the README or documentation with details of changes
3. Your pull request will be reviewed by the maintainers
4. Address any feedback or requested changes

### Code of Conduct
Please note that this project is released with a [Contributor Code of Conduct](https://www.contributor-covenant.org/version/2/0/code_of_conduct/). By participating, you are expected to uphold this code.

### Questions?
If you have any questions, please open an issue or contact the maintainers.

## License

This project is licensed under the Apache License, Version 2.0. 

A full copy of the license is available in the [LICENSE](LICENSE) file in the repository. 

Key terms of the Apache 2.0 License include:
- Permissions for commercial use
- Modification and distribution allowed
- Patent protection
- Trademark use restrictions
- No warranty

You can view the complete license details at [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0).