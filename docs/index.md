## Introduce
This is tienthuan19 handbook

## Target
BrainStormming & Solution solve all the challenges of the Juice Shop.

## Development Guide

This document guides you on how to set up the development environment for the **Juice Shop Handbook** on a new machine.

### Requisites
Ensure you have the following installed:

1.  **Git**
2.  **Python 3.10+**
3.  **Docker Desktop** (to run the target Juice Shop app)

### Quick Start

#### 1. Clone the Repository
```bash
git clone https://github.com/tienthuan19/juice-shop-handbook.git
cd juice-shop-handbook
```

#### 2. Setup Python Environment
Create a virtual environment to isolate dependencies.

Windows:
```bash
py -m venv venv
.\venv\Scripts\activate
pip install -r requirements.txt
```

Mac/Linux:

```Bash
py -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```
**Note:** If requirements.txt is missing, install manually: 
```bash
pip install mkdocs mkdocs-material mkdocs-awesome-pages-plugin
```

#### 3. Start the Target (Juice Shop)
Run the vulnerable application using Docker:

```Bash
docker run --rm -p 8080:3000 bkimminich/juice-shop
```
Access app at: http://localhost:8080


#### 4. Run the Handbook (MkDocs)
In a new terminal (with venv activated):

```Bash
mkdocs serve
```
Access handbook at: http://localhost:8000 (depending on your setup)
