import os
from git import Repo
from pathlib import Path

class RepoSniffer:
    def __init__(self, repo_path):
        self.repo_path = repo_path
        self.repo = Repo(repo_path)

    def get_commit_history(self):
        for commit in self.repo.iter_commits():
            print(f"Commit: {commit.hexsha}")
            print(f"Author: {commit.author.name} <{commit.author.email}>")
            print(f"Date: {commit.authored_datetime}")
            print(f"Message: {commit.message}\n")

    def list_files(self):
        print("List of Files:")
        for root, dirs, files in os.walk(self.repo_path):
            for file in files:
                print(os.path.join(root, file))

    def analyze_code(self):
        print("Code Analysis:")
        for root, dirs, files in os.walk(self.repo_path):
            for file in files:
                if file.endswith(".py"):  # Change the extension based on your needs
                    file_path = os.path.join(root, file)
                    with open(file_path, "r", encoding="utf-8") as f:
                        lines = f.readlines()
                        print(f"File: {file_path}")
                        print(f"Lines of Code: {len(lines)}")
                        print(f"Content: {lines}\n")

if __name__ == "__main__":
    repo_path = "path/to/your/repository"  # Replace with the actual path
    repo_sniffer = RepoSniffer(repo_path)

    print("Commit History:")
    repo_sniffer.get_commit_history()

    print("\nFile Listing:")
    repo_sniffer.list_files()

    print("\nCode Analysis:")
    repo_sniffer.analyze_code()
