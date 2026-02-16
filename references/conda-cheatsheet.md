# Conda Cheat Sheet for ML Engineering

## Environment Management

### Creating Environments
```bash
# Create new environment with specific Python version
conda create -n env_name python=3.11

# Create with specific packages
conda create -n env_name python=3.11 numpy pandas matplotlib

# Create from environment file
conda env create -f environment.yml

# Create from minimal/cross-platform file
conda env create -f environment-minimal.yml
```

### Activating/Deactivating
```bash
# Activate environment
conda activate env_name

# Deactivate current environment
conda deactivate

# Return to base environment
conda activate base
```

### Listing Environments
```bash
# List all environments
conda env list
# OR
conda info --envs

# Show currently active environment
echo $CONDA_DEFAULT_ENV  # Mac/Linux
echo %CONDA_DEFAULT_ENV%  # Windows
```

### Removing Environments
```bash
# Delete an environment completely
conda remove -n env_name --all

# Remove with confirmation prompt
conda env remove -n env_name
```

## Package Management

### Installing Packages
```bash
# Install single package
conda install numpy

# Install multiple packages
conda install numpy pandas matplotlib

# Install specific version
conda install numpy=1.24.3

# Install from specific channel
conda install -c conda-forge package_name

# Install in specific environment (without activating)
conda install -n env_name package_name
```

### Listing Packages
```bash
# List all packages in current environment
conda list

# Search for specific package
conda list numpy

# List packages with grep (Mac/Linux)
conda list | grep numpy

# List packages with findstr (Windows)
conda list | findstr numpy
```

### Updating Packages
```bash
# Update single package
conda update numpy

# Update all packages in environment
conda update --all

# Update conda itself
conda update conda

# Update Anaconda distribution
conda update anaconda
```

### Removing Packages
```bash
# Remove single package
conda remove numpy

# Remove multiple packages
conda remove numpy pandas

# Remove from specific environment
conda remove -n env_name package_name
```

## Exporting/Importing Environments

### Export Current Environment
```bash
# Full export (OS-specific, exact versions)
conda env export > environment.yml

# Minimal export (cross-platform, only explicitly installed)
conda env export --from-history > environment-minimal.yml

# Export without builds (more portable)
conda env export --no-builds > environment.yml
```

### Update Environment from File
```bash
# Update existing environment to match file
conda env update -f environment.yml

# Update and remove packages not in file
conda env update -f environment.yml --prune
```

### Clone Environment
```bash
# Create exact copy of existing environment
conda create -n new_env --clone existing_env
```

## Environment Information

### Get Details
```bash
# Show conda configuration
conda config --show

# Show environment info
conda info

# Show specific environment details
conda info -n env_name

# Show Python executable location
python -c "import sys; print(sys.executable)"
```

## Troubleshooting

### Common Issues and Fixes
```bash
# Clean conda cache (frees disk space)
conda clean --all

# Verify environment integrity
conda list --explicit

# Repair corrupted environment
conda install --revision 0  # Go to base revision

# Check for conflicts
conda list --revisions
```

### Environment Not Activating
```bash
# Reinitialize conda for your shell
conda init bash   # Linux/Git Bash
conda init zsh    # Mac
conda init pwsh   # Windows PowerShell

# Then restart terminal
```

### Reset Base Environment
```bash
# If base environment is corrupted
conda install --revision 0
conda update conda
```

## Performance & Configuration

### Speed Up Package Installation
```bash
# Use libmamba solver (much faster)
conda install -n base conda-libmamba-solver
conda config --set solver libmamba
```

### Channel Management
```bash
# Add channel with priority
conda config --add channels conda-forge

# Remove channel
conda config --remove channels conda-forge

# Show channel priority
conda config --show channels
```

## Useful Aliases (Add to Shell Config)

**For Mac/Linux (`~/.zshrc` or `~/.bashrc`):**
```bash
alias ca='conda activate'
alias cda='conda deactivate'
alias cel='conda env list'
alias cpl='conda list'
alias ci='conda install'
alias cu='conda update'
```

**For Windows PowerShell (`$PROFILE`):**
```powershell
function ca { conda activate $args }
function cda { conda deactivate }
function cel { conda env list }
function cpl { conda list }
```

## ML Engineering Workflow

### Typical Project Setup
```bash
# 1. Create project environment
conda create -n project_name python=3.11

# 2. Activate it
conda activate project_name

# 3. Install core ML packages
conda install numpy pandas matplotlib scikit-learn jupyter

# 4. Export for reproducibility
conda env export --from-history > environment-minimal.yml

# 5. Commit to git
git add environment-minimal.yml
git commit -m "Add project environment specification"
```

### Cross-Platform Team Workflow
```bash
# Developer 1 (creates environment)
conda create -n ml_project python=3.11 numpy pandas
conda env export --from-history > environment-minimal.yml
git push

# Developer 2 (different OS, reproduces environment)
git pull
conda env create -f environment-minimal.yml
conda activate ml_project
```

### Adding New Package (Team Workflow)
```bash
# Install new package
conda install scikit-learn

# Update environment file
conda env export --from-history > environment-minimal.yml

# Commit and push
git add environment-minimal.yml
git commit -m "Add scikit-learn to environment"
git push

# Teammates update their environments
git pull
conda env update -f environment-minimal.yml --prune
```

## Quick Reference

| Task | Command |
|------|---------|
| Create environment | `conda create -n name python=3.11` |
| Activate | `conda activate name` |
| Deactivate | `conda deactivate` |
| List environments | `conda env list` |
| Install package | `conda install package` |
| List packages | `conda list` |
| Export environment | `conda env export > env.yml` |
| Create from file | `conda env create -f env.yml` |
| Update environment | `conda env update -f env.yml --prune` |
| Remove environment | `conda remove -n name --all` |
| Clone environment | `conda create -n new --clone old` |

## Emergency Commands
```bash
# Environment completely broken? Start fresh:
conda deactivate
conda remove -n broken_env --all
conda env create -f environment.yml

# Conda itself broken? Reinstall:
# Download fresh Anaconda/Miniconda installer and reinstall

# Disk space issues?
conda clean --all
```

## Resources

- Official Conda Docs: https://docs.conda.io/
- Conda Cheat Sheet (PDF): https://docs.conda.io/projects/conda/en/latest/user-guide/cheatsheet.html
- Environment Best Practices: https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html

---

*For Git workflow, see `git-cheatsheet.md`*  
*For Python syntax, see `python-cheatsheet.md` (future)*