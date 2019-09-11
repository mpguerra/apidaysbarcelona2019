---
title: Introduction to Onion Services to secure APIs
subtitle: http < https < onion services 
date: September 12, 2019
author:
  - name: Pili Guerra
slides:
    aspect-ratio: 169
    font-size: 14pt
    table-of-contents: false
---

## About Me

\begin{columns}
    \begin{column}{0.65\textwidth}
        \begin{itemize}
            \item Project Manager at The Tor Project since September 2018.
            \item API Solution Engineer at 3scale and Red Hat since 2013.
            \item Worked with hundreds of customers to help them set up their API Program
        \end{itemize}
    \end{column}
    \begin{column}{0.35\textwidth}
        \begin{center}
            \includegraphics[width=0.95\textwidth]{images/pili-tor.jpg}
        \end{center}
    \end{column}
\end{columns}

## What is Tor?

\begin{columns}
    \begin{column}{0.4\textwidth}
        \begin{center}
            \includegraphics[width=0.95\textwidth]{images/what_is_tor.jpg}
        \end{center}
    \end{column}
    \begin{column}{0.6\textwidth}
        \begin{itemize}
            \item Open Source Software
            \item Network of servers run by volunteers
            \item Community of researchers, developers, users, and relay operators.
            \item U.S. 501(c)(3) non-profit organization.
        \end{itemize}
    \end{column}
\end{columns}

## Tor: Open Source Software

\begin{columns}
    \begin{column}{0.65\textwidth}
        \begin{itemize}
            \item Free Software: "Free as in Freedom"
            \item Written in C
            \item Follows best practices: 
            \begin{itemize}
                \item high coverage for tests
                \item integration tests
                \item coverity
                \item static code analysis
                \item code review policies
            \end{itemize}
            \item \href{https://gitweb.torproject.org/torspec.git}{Specification} and discussion before implementation.
        \end{itemize}
    \end{column}
    \begin{column}{0.35\textwidth}
        \begin{center}
            \includegraphics[width=0.95\textwidth]{images/tor-logo.png}
        \end{center}
    \end{column}
\end{columns}

## Tor: Network

\begin{columns}
    \begin{column}{0.5\textwidth}
        \begin{itemize}
            \item An open network -- everybody can join!
            \item Around 6,500 volunteer nodes
            \item Kindly hosted by various individuals, companies, and non-profit organisations.
            \item Between 2,000,000 and 8,000,000 daily users
        \end{itemize}
    \end{column}
    \begin{column}{0.5\textwidth}
        \begin{center}
            \includegraphics[width=0.95\textwidth]{images/relays.png}
        \end{center}
    \end{column}
\end{columns}

## Tor: Network

\centering
\begin{tikzpicture}
    \begin{axis}[
            title=Total Relay Bandwidth,
            title style={font=\scriptsize\bfseries},
            no markers,
            enlarge x limits=false,
            grid=both,
            grid style=dashed,
            width=0.85\paperwidth,
            height=0.80\paperheight,
            date coordinates in=x,
            xmin=2010-01-01,
            xmax=2019-01-01,
            xtick={
                {2010-01-01},
                {2011-01-01},
                {2012-01-01},
                {2013-01-01},
                {2014-01-01},
                {2015-01-01},
                {2016-01-01},
                {2017-01-01},
                {2018-01-01},
                {2019-01-01}
            },
            cycle list name=exotic,
            every axis plot/.append style={thick},
            label style={font=\scriptsize},
            tick label style={font=\scriptsize},
            legend style={
                font=\tiny,
            },
            legend pos=north west,
            legend cell align=left,
            unbounded coords=discard,
            xticklabel style={
                anchor=near xticklabel,
            },
            ylabel={Bandwidth in Gbit/s},
            xticklabel=\year\
            ]
        \addlegendentry{Advertised Bandwidth}
        \addplot table [x=date, y=advbw, col sep=comma] {data/bandwidth-flags_compressed.csv};
        \addlegendentry{Bandwidth History}
        \addplot table [x=date, y=bwhist, col sep=comma] {data/bandwidth-flags_compressed.csv};
    \end{axis}
\end{tikzpicture}

\tiny Source: \href{https://metrics.torproject.org/}{metrics.torproject.org}

## Tor: Network

\centering
\begin{tikzpicture}
    \begin{axis}[
            title=Number of Relays,
            title style={font=\scriptsize\bfseries},
            no markers,
            enlarge x limits=false,
            grid=both,
            grid style=dashed,
            width=0.85\paperwidth,
            height=0.80\paperheight,
            date coordinates in=x,
            xmin=2010-01-01,
            xmax=2019-01-01,
            xtick={
                {2010-01-01},
                {2011-01-01},
                {2012-01-01},
                {2013-01-01},
                {2014-01-01},
                {2015-01-01},
                {2016-01-01},
                {2017-01-01},
                {2018-01-01},
                {2019-01-01}
            },
            cycle list name=exotic,
            every axis plot/.append style={thick},
            label style={font=\scriptsize},
            tick label style={font=\scriptsize},
            legend style={
                font=\tiny,
            },
            legend pos=north west,
            legend cell align=left,
            unbounded coords=discard,
            xticklabel style={
                anchor=near xticklabel,
            },
            xticklabel=\year\
            ]
        \addlegendentry{Relays}
        \addplot table [x=date, y=relays, col sep=comma] {data/networksize.csv};
        \addlegendentry{Bridges}
        \addplot table [x=date, y=bridges, col sep=comma] {data/networksize.csv};
    \end{axis}
\end{tikzpicture}

\tiny Source: \href{https://metrics.torproject.org/}{metrics.torproject.org}

## {.plain}

\begin{center}
    \includegraphics[width=0.75\textwidth]{images/how-tor-works.png}
    \tiny Image credits: \href{https://twitter.com/micahflee}{@micahflee}
\end{center}    

## Tor Project, Inc

\begin{columns}
    \begin{column}{0.5\textwidth}
        \begin{itemize}
            \item US Non-Profit
            \item International and distributed team
            \item Dedicated to Privacy online
            \item Advocating for private access to the uncensored web
            \item \href{https://www.torproject.org/}{www.torproject.org}
        \end{itemize}
    \end{column}
    \begin{column}{0.5\textwidth}
        \begin{center}
            \includegraphics[width=0.95\textwidth]{images/tor-meeting-pic-stockholm.png}
        \end{center}
    \end{column}
\end{columns}

## {.plain}

\begin{tikzpicture}[remember picture,overlay, background rectangle/.style={fill=OnionDarkPurple}, show background rectangle]
    \node[text=white, at=(current page.north), yshift=-2.5cm, font=\bfseries] {\begin{tabular}{c} Our Mission: \\ To advance human rights and freedoms \\ by creating and deploying free and open source \\ anonymity and privacy technologies, \\ supporting their unrestricted availability and use, \\  and furthering their scientific and popular understanding. \end{tabular}};
    \node[at=(current page.center), yshift=-2.5cm, align=center] {\input{images/tor_group.tex}};
\end{tikzpicture}

## {.plain}

\begin{tikzpicture}[remember picture,overlay, background rectangle/.style={fill=white}, show background rectangle]
    \node[text=OnionDarkPurple, at=(current page.north), yshift=-2.5cm, font=\bfseries] { This is all great... but what does it have to do with API security?!?! };
\end{tikzpicture}

## .Onion Services

\begin{columns}
    \begin{column}{0.6\textwidth}
        \begin{itemize}
            \item Configured to receive inbound connections only through Tor
            \item Traffic stays within the Tor network: No need to exit the network.
            \item ".onion" Special-Use Domain Name (\href{https://tools.ietf.org/html/rfc7686}{RFC 7686}).
            \item Allow clients and servers to be anonymous.
            \item Can be used for all kinds of TCP traffic
        \end{itemize}
    \end{column}
    \begin{column}{0.4\textwidth}
        \begin{center}
            \includegraphics[width=0.95\textwidth]{images/Onion_Color.png}
        \end{center}
    \end{column}
\end{columns}

## {.plain}

\begin{center}
    \includegraphics[width=0.75\textwidth]{images/how-onion-services.png}
    \tiny Image credits: \href{https://twitter.com/micahflee}{@micahflee}
\end{center}

## .Onion Services: Properties

\begin{columns}
    \begin{column}{0.5\textwidth}
        \begin{center}
            \includegraphics[width=0.95\textwidth]{images/onion-services.png}
        \end{center}
    \end{column}
    \begin{column}{0.5\textwidth}
        \begin{itemize}
            \item Self authenticated.
            \item End-to-end encrypted.
            \item Isolation and NAT punching.
            \item Minimized attack surface.
            \item Censorship resistant
            \begin{itemize}
                \item no DNS or BGP hijacking/poisoning
            \end{itemize}
            \item Support for Unix domain sockets.
        \end{itemize}
    \end{column}
\end{columns}

## Self Authentication

\begin{columns}
    \begin{column}{0.6\textwidth}
        \begin{itemize}
            \item .onion service addresses are a hash of the service's public-key
            \item No need for a centralized Certificate Authority (CA)
            \item Clients can be assured they’re talking to the correct host
            \item Makes MITM attacks impossible
        \end{itemize}
    \end{column}
    \begin{column}{0.4\textwidth}
        \begin{center}
            \includegraphics[width=0.95\textwidth]{images/browse-freely.png}
        \end{center}
    \end{column}
\end{columns}


## End-to-end Encryption

\begin{columns}
    \begin{column}{0.6\textwidth}
        \begin{itemize}
            \item Requests are protected by 3 layers of encryption
            \item Request metadata is hidden
            \item Source, content and destination all encrypted
            \item Confidential data sharing
        \end{itemize}
    \end{column}
    \begin{column}{0.4\textwidth}
        \begin{center}
            \includegraphics[width=0.95\textwidth]{images/encryption.png}
        \end{center}
    \end{column}
\end{columns}

## {.plain}

\begin{center}
    \includegraphics[width=0.75\textwidth]{images/https-tor.png}
    \tiny Image credits: \href{https://www.eff.org/pages/tor-and-https}{www.eff.org}
\end{center}

## {.plain}

\begin{tikzpicture}[remember picture,overlay, background rectangle/.style={fill=OnionDarkPurple}, show background rectangle]
    \node[text=white, at=(current page.north), yshift=-2.5cm, font=\bfseries] { http < https < onion services };
    \node[at=(current page.center), yshift=-2.5cm, align=center] {\input{images/tor_group.tex}};
\end{tikzpicture}

## .onion > https

\begin{columns}
    \begin{column}{0.6\textwidth}
        \begin{itemize}
            \item https doesn't hide request metadata
            \item https doesn't hide your location
            \item https doesn't hide network metadata
            \item https doesn't hide who you are exchanging data with
        \end{itemize}
    \end{column}
    \begin{column}{0.4\textwidth}
        \begin{center}
            \includegraphics[width=0.95\textwidth]{images/block.png}
        \end{center}
    \end{column}
\end{columns}    

## Use cases 

\begin{columns}
    \begin{column}{0.5\textwidth}
        \begin{center}
            \includegraphics[width=0.95\textwidth]{images/use-cases.png}
        \end{center}
    \end{column}
    \begin{column}{0.5\textwidth}
        \begin{itemize}
            \item Health Sector
            \item Government Services
            \item Tip-lines / Abuse complaints
            \item Chinese walls within companies
            \item Securing vulnerable infrastructure
            \item IoT
        \end{itemize}
    \end{column}
\end{columns}    

## {.plain}

\begin{tikzpicture}[remember picture,overlay, background rectangle/.style={fill=OnionDarkPurple}, show background rectangle]
    \node[text=white, at=(current page.north), yshift=-2.5cm, font=\bfseries] { Demo Time: Onionizing your API };
    \node[at=(current page.center), yshift=-2.5cm, align=center] {\input{images/tor_group.tex}};
\end{tikzpicture}

## {.c .plain .noframenumbering}

\centering

\vfill

\huge Questions?

\vfill

\includegraphics[width=0.4\textwidth]{images/outreach.png}

## {.c .plain .noframenumbering}

\centering

This work is licensed under a

\large \href{https://creativecommons.org/licenses/by-sa/4.0/}{Creative Commons \\ Attribution-ShareAlike 4.0 International License}

\vfill

\ccbysa

\vfill