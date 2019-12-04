# Project Assigner GitHub Action

This is a GitHub action, implemented in JavaScript, which does the following:
  - Assigns an issue or pull request to a project when a specified label is applied
  - Removes an issue or pull request from a project when a specified label is removed

You can provide multiple lable to project mappings as the action input.

## Inputs

### `issue-mappings`
A JSON array of objects containing `label`, `projectName`, and `columnId` attributes.

**`label`** - name of the GitHub lable that should trigger this action when it's applied to or removed from an issue or a pull request.

**`projectName`** - name of the project that an issue or pull request should be assinged to when the label is applied, or removed from when the label is removed.

**`columnId`** - *ID* of the GitHub project column that an issue or a pull request should be placed in when they're assigned to the project.  For issues, this would typically be the ID of the "To Do" column. For pull requests, this may be the ID of the "In Review" column. You should use your own discression when choosing which columns to use for your particular project.  A column ID can be found by copying the column URL using its "..." menu and then using the numeric ID at the end of the URL as the value for `columnId`.

Here's a sample format of the `issue-mappings` input:

	issue-mappings: '[{"label": "Test", "projectName": "test", "columnId": 1234},
            {"label": "bug", "projectName": "test2", "columnId": 5678}]'

## Example usage
	uses: alexh97/github-actions/project-assigner@v1
	with:
	  issue-mappings: '[{"label": "Test", "projectName": "test", "columnId": 1234},
	    {"label": "bug", "projectName": "test2", "columnId": 5678}]'

