import re
import os
from github import Github

# Define the regex pattern
COMMIT_REGEX = re.compile(r"^(build|chore|ci|docs|feat|fix|perf|refactor|revert|style|test){1}(\([\w]+\))?(!)?: (.*)$")

# Read commit messages from the file
with open("commit_messages.txt", "r") as f:
    commit_messages = f.readlines()

invalid_commits = []

for line in commit_messages:
    commit_hash, commit_message = line.split(" ", 1)
    if not COMMIT_REGEX.match(commit_message.strip()):
        invalid_commits.append(f"{commit_hash}: {commit_message.strip()}")

# Save invalid commit messages to a file for GitHub Action annotations
with open("invalid_commits.txt", "w") as f:
    f.write("\n".join(invalid_commits))

# Exit with an error if invalid commits are found
if invalid_commits:
    print("Invalid commit messages found:")
    for commit in invalid_commits:
        print(commit)
    exit(1)
else:
    print("All commit messages are valid.")
