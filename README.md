# bazel-user-root-rebuild-bug

On MacOS if you're building this project with :
```bash
bazel --output_user_root=~/Library/Caches/my_bazel_cache/ build //:test -s
```

Then change `test.h` header file and rebuild it will not re-compile anything
```bash
echo "" > test.h
# Building should now throw a compilation error, but nothing gets re-compilled
bazel --output_user_root=~/Library/Caches/my_bazel_cache/ build //:test -s
# Note that building without $USER set will work
USER="" bazel --output_user_root=~/Library/Caches/my_bazel_cache/ build //:test -s
```
