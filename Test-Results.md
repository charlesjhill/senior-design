# Test Results

*For a description of tests, please refer to the [Test Plan](<Overall Test Plan.docx>)*

## OCG1

The Operating Characteristic (OC) generator correctly ingests a schema into a Probabilistic Graphical Model (PGM).

## OCG2

The OC generator validation functionality is working as expected, detecting abnormal schemas and ensuring valid PGMs.

## OCG3

Forward sampling the PGM works as expected, producing valid "bags" of OCs for later use.

## OCG4

After inspecting the target SQLite3 database file, the OC generator is correctly persisting bags of OCs for later ingestion and use

## OCG5

The entire OC generation pipeline, from a human-validated schema (in the form of an excel file), to its eventual output in a persisted database, is operational, providing a key cornerstone for future work.

## OCG6

Following some work on optimizing the database persistence, 200 samples were generated in 6.59 seconds (=30.35 samples/sec). Given the fixed 2 second overhead of the generation process, the performance as the number of samples approaches infinity is even better. The target was 30 samples/sec, so this is a pass.

## SDG1

Not only are samples being persisted to the database, but the next step of pipeline reads them out correctly, as deduced by software introspection.

## SDG2

The system generates .NITF formatted imagery, which is what is expeceted for SAR data.

## DL1

A custom-written DataLoader was created to ingest the .NITF data and convert it into single-channel pixel data. These are then written out to JPEG files for later ingestion. This passes.

## DM1

During the course of the project, Bhattacharyya distance ended up getting unused in favor of the Kullbacck-Leibler (KL) divergence, so this test was rendered no longer applicable.

## DM2

KL Divergence is implemented as a standard library functionn of SciPy - `rel_entr`. The Scipy's unit test suite demonstrates this function as working as expected.

## DNN1

Trials suggests we were able to train a ResNet50 model - with tweaks to ingest our data format (100x100 with 1 channel) and output our desired number of classes, among other light alterations - within reasonable expectations given the complexity of the model and sophistication of its training data. Validation scores tended to improve as more features of the validation set were introduced into the testing set, demonstrating that the training pipeline was working as expected.