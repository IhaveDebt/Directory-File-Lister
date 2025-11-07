#include <stdio.h>
#include <dirent.h>
#include <sys/stat.h>

int main() {
    DIR *dir;
    struct dirent *entry;
    struct stat info;
    char path[1024] = ".";

    dir = opendir(path);
    if (!dir) {
        perror("Cannot open directory");
        return 1;
    }

    printf("Files in directory '%s':\n", path);
    while ((entry = readdir(dir)) != NULL) {
        stat(entry->d_name, &info);
        printf("%-20s\t%ld bytes\n", entry->d_name, info.st_size);
    }

    closedir(dir);
    return 0;
}
