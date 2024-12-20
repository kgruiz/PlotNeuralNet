# PlotNeuralNet

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.2526396.svg)](https://doi.org/10.5281/zenodo.2526396)

**PlotNeuralNet** is a Python package that provides tools to generate high-quality neural network architecture diagrams for research papers, presentations, and reports. It leverages LaTeX and Python for seamless integration into scientific workflows.

This package is based on the original **[PlotNeuralNet by HarisIqbal88](https://github.com/HarisIqbal88/PlotNeuralNet)**, with improvements for better usability and a modular package structure.

---

## **Features**
- Programmatically generate neural network diagrams using Python.
- Predefined layer types (e.g., Conv, Pool, SoftMax).
- Easily extendable for custom layer shapes.
- Pre-built LaTeX templates for popular architectures like AlexNet, FCN, and HED.
- Fully structured as a Python package for streamlined integration into projects.

---

## **Getting Started**

### **Installation**

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/PlotNeuralNet.git
   cd PlotNeuralNet
   ```

2. Install the package:
   ```bash
   pip install .
   ```

3. Verify the installation:
   ```python
   import PlotNeuralNet
   print("PlotNeuralNet installed successfully!")
   ```

---

## **Usage**

The package is organized to simplify the creation of diagrams. It includes Python modules (`pycore` and `pyexamples`) and LaTeX resources (`layers`).

### **1. Python Usage**

#### **Define an Architecture**
You can use the Python API to define your architecture programmatically. For example:

```python
from PlotNeuralNet.pycore import tikzeng
from PlotNeuralNet.pycore.blocks import block_2ConvPool, block_Unconv

# Define architecture
arch = [
    tikzeng.to_head('..'),
    tikzeng.to_cor(),
    tikzeng.to_begin(),

    # Input image
    tikzeng.to_input('../examples/fcn8s/cats.jpg'),

    # Encoder
    *block_2ConvPool(name='b1', botton='input', top='b2', s_filer=256, n_filer=64),
    *block_2ConvPool(name='b2', botton='b2', top='b3', s_filer=128, n_filer=128),

    # Decoder
    *block_Unconv(name='b4', botton='b3', top='output', s_filer=64, n_filer=32),

    # Output layer
    tikzeng.to_ConvSoftMax(name='softmax', offset="(1,0,0)", to="(output-east)", width=1, height=30, depth=30),
    tikzeng.to_end(),
]

# Generate the architecture diagram
def main():
    tikzeng.to_generate(arch, "my_architecture.tex")

if __name__ == "__main__":
    main()
```

#### **Compile and View the Diagram**
Run the Python script:
```bash
python my_architecture.py
```

Compile the `.tex` file with:
```bash
bash ../tikzmake.sh my_architecture
```

---

### **2. LaTeX Usage**

You can directly modify `.tex` files in the `examples` directory, such as `examples/FCN-8` or `examples/HED`. Each `.tex` file demonstrates how to use LaTeX for defining architectures.

To compile a `.tex` file, use:
```bash
pdflatex <file>.tex
```

---

### **3. Access Predefined Resources**
The package structure includes predefined resources for easy reuse:

#### **LaTeX Resources**
- Available in the `PlotNeuralNet/layers/` directory.
- Example LaTeX layer definitions:
  ```latex
  \input{layers/Box.sty}
  ```

#### **Examples**
- Predefined architectures like FCN, HED, AlexNet are in `PlotNeuralNet/examples/`.
- Modify these examples to fit your use case.

#### **Python Scripts**
- Python examples for generating diagrams programmatically are in `PlotNeuralNet/pyexamples/`.
- Example usage:
  ```bash
  python PlotNeuralNet/pyexamples/unet.py
  ```

---

## **Package Structure**

The package is organized as follows:

```
PlotNeuralNet/
├── LICENSE          # License file
├── MANIFEST.in      # File inclusion rules
├── README.md        # Documentation
├── setup.py         # Installation script
├── PlotNeuralNet/   # Main package directory
│   ├── __init__.py  # Package initializer
│   ├── pycore/      # Core Python modules
│   ├── layers/      # LaTeX resources
│   ├── examples/    # Predefined architectures in LaTeX
│   ├── pyexamples/  # Python examples
├── dist/            # Build artifacts (after running setup.py)
├── build/           # Temporary build files
```

---

## **Advanced Features**

1. **Custom Layers**
   - Extend `pycore.blocks` or create your own block definitions to support custom layers.

2. **Batch Processing**
   - Use Python scripts to generate multiple architectures programmatically.

3. **Predefined Functions**
   - `block_2ConvPool` and `block_Unconv` simplify common layer patterns.

---

## **Acknowledgments**

This package is based on the original **[PlotNeuralNet by HarisIqbal88](https://github.com/HarisIqbal88/PlotNeuralNet)** and licensed under the MIT License.

---

## **License**

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for more details.