# Probator
Probator is a C++ tool for turning untrusted files into clean ones. It doesn't try to spot malware. Instead it takes a file apart inside a sandbox, keeps only the content it understands, checks that content outside the sandbox, and builds a brand-new file from it.

# The problem

Files are a common way to deliver attacks. A file can look completely normal and still carry something hidden:

* Extra data appended after the real content (for example, a ZIP glued onto the end of a JPEG) 
* scripts, macros or embedded objects
* metadata such as GPS location
* malformed structures designed to crash or take over the program that reads them

The obvious defence is a scanner that looks for known bad things and removes them. That approach always lags behind attackers, because it has to recognise every trick in advance.

# The approach: Content Disarm and Reconstruction (CDR)

Probator follows the opposite approach, known as Content Disarm and Reconstruction:

* Disarm: parse the input and extract only the content that's actually needed (for an image, the pixels).
* Reconstruct: build a completely new file from that content.

Anything that wasn't deliberately carried over never reaches the output: hidden payloads, appended data and metadata all disappear, even if nobody knew they were there. The question changes from "is this file bad?" to "is this exactly what I expect?"
