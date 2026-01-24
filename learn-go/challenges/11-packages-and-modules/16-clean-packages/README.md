# clean packages

Challenge: 16-clean-packages
Chapter: 11-packages-and-modules

I've often seen, and have been responsible for, throwing code into packages without much thought. I've quickly drawn a line in the sand and started putting code into different directories (wich in Go are different packages by definition) just for teh sake or organization. *Learning to properly build small and reusable packages can take your Go career to the next level*.

# Rules of Thumb

1. Hide Internal logic

If you're familiar with the pillars of OOP, this is a practice in *encapsulation*.

Oftentimes an application will have complex logic that requires a lot of code. In almost every case the logic that the application cares about can be exposed via an API, and most of the dirty work can be kept within a package. For example, imagine we are builing an application that needs to classify images. We could build a package.

```go
package classifier

// ClassifyImage classifies images as "hotdog" or "not hotdog"
func ClassifyImage(image []byte) (imageType string) {
    if hasHotdogColors(image) && hasHotdogShape(image) {
        return "hotdog"
    } else {
        return "not hotdog"
    }
}

func hasHotdogShape(image []byte) bool {
    // Internal logic that the application doesn't need to know about
    return true
}

func hasHotdogColors(image []byte) bool {
    // Internal logic that the application doesn't need to know about
    return true
}
```

We create an API by only exposing the function(s) that the application-level needs to know about. All other logic is unexported to keep a clean separation of concerns. The application doesn't need to know how to classify an image, just the result of the classification. Remember, in Go, functions with names starting with a lowercase letter are unexported and private to the package, while functions starting with an uppercase letter are exported and can be accessed externally.

2. Don't Change APIs

The unexported functions within a package can and should change often for testing, refactoring, and bug fixing.

A well-designed library will have a stable API so that users don't get breaking changes each time they update the package version. In Go, this means not changing exported function's signatures.

3. Don't Export Functions from the Main Package

A `main` package isn't a library, there's no need to export functions from it.

4. Packages Shouldn't Know About Dependants

Perhaps one of the most important and most borken rules is that a package shouldn't know anything about its Dependants. In other words, a package should never have specific knowledge about a particular application it uses.

## Question 1

Should you export code from the main package?

## Answer 1

- [ ] Yup
- [x] Nope

## Question 2

When should you NOT export a function, variable, or type?

## Answer 2

- [x] When the end-ser doesn't need to know about it.
- [ ] Never, its better to share code!

## Question 3

Should you often change a package's exported API?

## Answer 3

- [ ] Yes, move fast and break things
- [x] No, try to keep changes to internal functionality
- [ ] If the package is `main` then yes
