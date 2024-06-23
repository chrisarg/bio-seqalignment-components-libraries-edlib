# NAME

Bio::SeqAlignment::Components::Libraries::edlib - edlib library for developing sequence alignment tools

# VERSION

version 0.03

# SYNOPSIS

    use Bio::SeqAlignment::Components::Libraries::edlib;
    my $ffi = Bio::SeqAlignment::Components::Libraries::edlib->new_edlib_aligner();
    my $configuration = Bio::SeqAlignment::Components::Libraries::edlib->configure_edlib_aligner( $ffi, %config );
    my $align = Bio::SeqAlignment::Components::Libraries::edlib->edlibAlign( $query_seq, $query_len, $ref_seq, $ref_seq_len, $configuration->{edlib_config} );
    Bio::SeqAlignment::Components::Libraries::edlib->edlibFreeAlignResult( $align );

# DESCRIPTION

This module provides a Perl interface to the edlib library for developing sequence
alignment tools. The edlib library is a C/C++ library for sequence alignment using 
edit distance. It supports three alignment modes: global (Needleman-Wunsch), 
semi-global, and local (Smith-Waterman). 
This module provides a Perl interface to the edlib library for developing sequence
alignment tools. This particular module is meant to be used as a component in a
larger sequence alignment tool, e.g. one that combines a Linear dataflow and a 
generic sequence mapper. Currently only the alignment score is returned. 
Future versions will include the alignment path and the alignment locations in 
order to handle multiple/overlapping hits.

# METHODS

## new\_edlib\_aligner

    my $ffi = Bio::SeqAlignment::Components::Libraries::edlib->new_edlib_aligner();

This method creates a new FFI::Platypus object that can be used to call the functions
from the edlib library. The FFI::Platypus object is returned.

## configure\_edlib\_aligner

    my $configuration = Bio::SeqAlignment::Components::Libraries::edlib->configure_edlib_aligner( $ffi, %config );

This method configures the edlib aligner with the specified configuration. The configuration
is passed as a hash with the following keys: mode, task, filter, additionalEqualities, and
additionalEqualitiesLength. The configuration is returned as a hash reference with two keys:
edlib\_config and align\_config. The edlib\_config key contains the configuration for the edlib
aligner, while the align\_config key contains the configuration for the alignment.

## edlibAlign

    my $align = Bio::SeqAlignment::Components::Libraries::edlib->edlibAlign( $query_seq, $query_len, $ref_seq, $ref_seq_len, $configuration->{edlib_config} );

This method performs the sequence alignment using the edlib library. It takes as input the
query sequence, the length of the query sequence, the reference sequence, the length of the
reference sequence, and the configuration for the edlib aligner. It returns the alignment
result as a hash reference.

## edlibFreeAlignResult

    Bio::SeqAlignment::Components::Libraries::edlib->edlibFreeAlignResult( $align );

This method frees the memory allocated for the alignment result.

# EXPORTS

The following constants are exported by default:

- EDLIB\_STATUS\_OK
- EDLIB\_STATUS\_ERROR

The following functions are exported by the 'functions' tag:

- configure\_edlib\_aligner
- edlibNewAlignConfig
- edlibAlign
- edlibFreeAlignResult
- new\_edlib\_aligner

The following records are exported by the 'records' tag:

- EdlibEqualityPair
- EdlibAlignResult
- EdlibAlignConfig

# SEE ALSO

- [Alien::SeqAlignment::edlib](https://metacpan.org/pod/Alien%3A%3ASeqAlignment%3A%3Aedlib)
- [Bio::SeqAlignment::Components::Libraries::edlib::OpenMP](https://metacpan.org/pod/Bio::SeqAlignment::Components::Libraries::edlib::OpenMP);

    An alternative implementation of the edlib library that uses OpenMP for thread level parallelism

# TODO

- Add support for obtaining/parsing the alignment path
- Add support for obtaining/parsing the alignment locations
- Add support for mapping multiple and/or overlapping hits

# AUTHOR

Christos Argyropoulos <chrisarg@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2024 by Christos Argyropoulos.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
