# PyCharm Configuration Backup Tool

A command-line utility that helps you backup and restore PyCharm project configurations, recent projects lists, and global IDE settings. "Inspired" after a recent PyCharm upgrade lost configuration settings for my projects.

## Overview

This tool solves the problem of preserving your PyCharm settings and configurations across multiple machines or when reinstalling your development environment. It targets the `.idea` directories, recent projects lists, and global IDE settings files that aren't typically included in version control.

## Features

- **Project Configuration Backup**: Preserves your run configurations, Python interpreter settings, VCS settings, and more
- **Recent Projects List**: Keep your project history intact when migrating to a new machine
- **Global IDE Settings**: Backup code styles, templates, and other IDE preferences
- **Selective Restore**: Restore configurations for specific projects or all projects
- **Flexible Output**: Store backups in your preferred directory
- **Preview Changes**: View differences before applying restored configurations
- **Cross-Platform**: Works on Windows, macOS, and Linux

## Installation

```bash
# Clone the repository
git clone https://github.com/StephenGenusa/pycharm-configuration-backup.git
cd pycharm-config-backup

# Make the script executable (Linux/macOS)
chmod +x pycharm_config_backup.py

# Optional: Create a symlink for easier access
ln -s $(pwd)/pycharm_config_backup.py /usr/local/bin/pycharm-backup
```

## Usage

### Basic Commands

```bash
# Create a backup using default settings (projects in standard location)
./pycharm_config_backup.py --backup

# Restore a specific project from a backup
./pycharm_config_backup.py --restore-project "MyProject"

# Restore all projects from a backup
./pycharm_config_backup.py --restore-project all

# List available backups
./pycharm_config_backup.py --list-backups

# Run in interactive mode with a menu-driven interface
./pycharm_config_backup.py --interactive
```

### Advanced Options

```bash
# Specify projects directory and output directory
./pycharm_config_backup.py --backup --pycharm-projects-directory ~/Projects --output-directory ~/Backups

# Include global IDE settings in the backup
./pycharm_config_backup.py --backup --global-settings-backup

# Perform a dry-run restore to see what would happen
./pycharm_config_backup.py --restore-project "MyProject" --dry-run

# Show differences before restoring files
./pycharm_config_backup.py --restore-project "MyProject" --show-diff

# Filter which files to backup with include/exclude patterns
./pycharm_config_backup.py --backup --include "*.xml,*.iml" --exclude "workspace.xml"

# Restore only recent projects lists
./pycharm_config_backup.py --restore-recent-only

# Restore only global settings
./pycharm_config_backup.py --restore-global-only
```

## Configuration

The tool automatically detects your PyCharm project directories based on your operating system:

- **Windows**: `%APPDATA%\JetBrains` and `~\PyCharmProjects` or `Documents\PyCharmProjects`
- **macOS**: `~/Library/Application Support/JetBrains` and `~/PycharmProjects`
- **Linux**: `~/.config/JetBrains` and `~/PycharmProjects`

Configuration preferences are saved to `~/.pycharmbackuprc` for future use.

## Command-Line Arguments

| Argument | Description |
|----------|-------------|
| `-b`, `--backup` | Create a backup of PyCharm configurations |
| `-r PROJECT`, `--restore-project PROJECT` | Restore configuration for a specific project (or 'all') |
| `-l`, `--list-backups` | List available backups |
| `-i`, `--interactive` | Run in interactive mode with a menu |
| `-p DIR`, `--pycharm-projects-directory DIR` | Directory containing PyCharm projects |
| `-o DIR`, `--output-directory DIR` | Directory where backups will be stored (default: current directory) |
| `--output-file FILE` | Custom filename for the backup |
| `--dry-run` | Show what would be done without making changes |
| `--show-diff` | Show differences before restoring files |
| `--include PATTERNS` | Comma-separated list of patterns to include (e.g., '*.xml,*.iml') |
| `--exclude PATTERNS` | Comma-separated list of patterns to exclude (e.g., 'workspace.xml') |
| `--max-backups N` | Maximum number of backups to keep (0 = keep all) |
| `-gs`, `--global-settings-backup` | Include global IDE settings in backup |
| `--restore-recent` | Also restore recent projects list when restoring a project |
| `--restore-global` | Also restore global IDE settings when restoring a project |
| `--log-file FILE` | Log to the specified file |
| `-v`, `--verbose` | Enable verbose logging |
| `-q`, `--quiet` | Suppress normal output (errors will still be displayed) |

## Tips

- Run a `--dry-run` before restoring to ensure you're not overwriting important configurations
- Use `--show-diff` to examine changes before applying them
- For team projects, exclude personal configuration files like `workspace.xml` when creating backups
- The interactive mode (`-i`) is recommended for first-time users to explore the tool's capabilities

## Troubleshooting

**Q: The tool doesn't find my PyCharm projects**  
A: Use the `--pycharm-projects-directory` option to specify your non-standard project location.

**Q: I get permission errors during restore**  
A: Close PyCharm before restoring, as it may lock configuration files.

**Q: Backup file is large**  
A: Use the `--exclude` option to skip large or unnecessary files.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Acknowledgments

- Built with Python's standard library for maximum compatibility