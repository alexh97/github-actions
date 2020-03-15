# Project Assigner GitHub Action

This is a GitHub action, implemented in JavaScript, which does the following:
  - Assigns an issue or pull request to a project when a specified label is applied
  - Removes an issue or pull request from a project when a specified label is removed

You can provide multiple label to project mappings as the action input.

## Inputs

### `issue-mappings`
A JSON array of objects containing `label`, `projectNumber`, and `columnName` attributes.

**`label`** - name of the GitHub label that should trigger this action when it's applied to or removed from an issue or a pull request.

**`projectNumber`** - number of the project that an issue or pull request should be assinged to when the label is applied, or removed from when the label is removed.

**`columnName`** - Name of the GitHub project column that an issue or a pull request should be placed in when they're assigned to the project.  For issues, this would typically be the "To Do" column. For pull requests, this may be the "In Review" column. You should use your own discression when choosing which columns to use for your particular project.  

Here's a sample format of the `issue-mappings` input:

	issue-mappings: '[{"label": "Test", "projectNumber": 1, "columnName": "To do"},
            {"label": "bug", "projectNumber": 2, "columnName": "In progress"}]'

## Example usage

In order to use this action, create a workflow configuration file (e.g. `issues-workflow.yml`) in your repository's `.github/workflows` directory. *Note that you need to have GitHub Actions enabled for your repository in order for this to work!*

### A workflow configuration for assigning issues to projects

	on:
  	  issues:
    	  types: [labeled, unlabeled]

	jobs:
	  assign_to_project:
	    runs-on: ubuntu-latest
	    name: Assign an issue to project based on label
	    steps:
	      - name: Assign to project
		uses: alexh97/github-actions/project-assigner@v1.0.0
		id: project_assigner
		with:
		  issue-mappings: '[{"label": "Test", "projectNumber": 1, "columnName": "To do"},
		    {"label": "bug", "projectNumber": 2, "columnName": "In progress"}]'
		  ghToken: ${{ secrets.GITHUB_TOKEN }}

### A workflow configuration for assigning pull requests to projects

	on:
	  pull_request:
	    types: [labeled, unlabeled]

	jobs:
	  assign_to_project:
	    runs-on: ubuntu-latest
	    name: Assign a PR to project based on label
	    steps:
	      - name: Assign to project
		uses: alexh97/github-actions/project-assigner@v1.0.0
		id: project_assigner
		with:
		  issue-mappings: '[{"label": "Test", "projectNumber": 1, "columnName": "In review"},
		    {"label": "enhancement", "projectNumber": 2, "columnName": "To do"}]'
		  ghToken: ${{ secrets.GITHUB_TOKEN }}
